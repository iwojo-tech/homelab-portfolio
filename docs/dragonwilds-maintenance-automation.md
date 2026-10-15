# Dragonwilds Maintenance Automation

**Home Assistant · Bash · Docker Compose · SteamCMD · Backups · Operational visibility**

## Why I built it

Hosting a private RuneScape: Dragonwilds server gave my homelab a workload that someone else depended on. A friend and I used the server, so maintenance affected both availability and the world we had built together.

A major reason for building these controls was to run maintenance and upgrade commands remotely, including when I was away from home. I wanted to check the server, restart it, or begin an update without having to wait until I was back home.

Making those actions accessible from my Home Assistant dashboard also saved me from opening an SSH session and remembering the same commands each time. Status, uptime, restart, and update controls brought the routine tasks into one place. As I developed the scripts and wrappers behind those controls, the project became an exercise in defining what a maintenance action should do, how it should report progress, and what should happen when it failed.

## Starting with a simple SSH button

The original Home Assistant button was straightforward: it opened an SSH connection and ran the restart command for Dragonwilds. Restarting the workload automatically triggered its startup SteamCMD check, so the button also provided a convenient way to initiate that check.

That first version made an existing task easier to perform. The SteamCMD behavior was already part of startup; the button gave me a way to trigger it from the dashboard.

As I expanded the controls, I needed more information than whether the restart command had been sent. I wanted to know whether SteamCMD was verifying or downloading files, whether the world had loaded, and when players could join again. The scripts and wrappers grew around those questions, adding a defined maintenance sequence and a record of its progress.

## Connecting the dashboard to the maintenance workflow

The dashboard provided a convenient place to request an action and see server information. The scripts and wrappers behind it gave those actions a repeatable procedure. That separation mattered: a button labeled “Update” needed a clear meaning, and the server-side procedure needed to remain understandable when I was troubleshooting from a terminal.

<p align="center">
  <a href="../images/homeassistant_dashboard_v2.png">
    <img src="../images/homeassistant_dashboard_v2.png" alt="Home Assistant dashboard with Dragonwilds controls and homelab service shortcuts" width="720">
  </a>
</p>

<p align="center"><em>The dashboard brings Dragonwilds controls and server information into the same place as the rest of my homelab.</em></p>

The container update script, `/usr/local/sbin/dragonwildsCT-update`, runs inside the Dragonwilds VM, identified as VM 200 in Proxmox. Despite the `CT` in the script name, this operation updates the Docker workload inside the VM.

## Turning an update into a defined procedure

The update workflow pulls the Docker image while the server remains online, then stops the container before backing up its saved world. It checks that the compressed archive can be read before starting the workload with Docker Compose. Finally, it follows the container logs for SteamCMD activity and application startup.

This introduced two separate update layers to keep track of: pulling the Docker image and letting SteamCMD check the game files during startup. The original restart button triggered the startup check; the later container update procedure also explicitly pulls the image and protects the saved world before starting the workload again.

Pulling the image first keeps that download outside the planned downtime. Stopping the server before copying its saves reduces the risk of archiving files while they are being changed. Backups live outside the application directory, with dated filenames and retention cleanup after a new archive passes its readability check.

That check has a specific limit: successfully listing an archive proves it is readable, but does not prove the world can be restored and loaded. A restore test remains a separate recovery exercise.

The script also takes a maintenance lock before proceeding. The purpose is to serialize cooperating maintenance scripts so that an update and a restart cannot work on the same server at the same time. The dashboard makes repeated requests easy, which makes coordination behind those controls more important.

## Learning what “ready” means

One of the most useful distinctions in this project was between Docker starting a container and Dragonwilds becoming available to players.

After startup, SteamCMD may still be checking or downloading game files. The application then needs to launch, load the world, and establish its online session. Returning successfully from `docker compose up -d` does not establish that all of those steps have completed.

The update script follows startup messages and waits for the application's `ReadyToJoin` marker before reporting success. It records a timestamp immediately before starting the container and reads logs from that point, reducing the chance that an old readiness message could satisfy the current update.

The monitor has a 45-minute limit. If readiness is not observed, the script distinguishes a stopped container from a container that is still running without confirmed readiness. This gave the workflow a more useful completion condition than a fixed sleep followed by a success message.

## What the real logs changed

The earlier progress handler looked for bracketed integer percentages such as `[42%]`. Captures from an actual startup showed a different format:

```text
Update state (0x5) verifying install, progress: 99.97
Update state (0x61) downloading, progress: 1.66
```

Those lines contain decimal percentages without a percent sign. The original pattern would miss them, even though the underlying update could still be progressing normally.

I replaced the generic handler with separate patterns for verification and downloading. Each captures the complete integer or decimal value and records both the stage and its percentage. This also explains why the displayed progress can move from almost 100 percent back to a small number: verification and downloading are separate stages, each with its own progress.

The change reinforced a practical troubleshooting lesson: build the parser around captured application output. A plausible pattern is only useful if it matches the messages the service actually produces.

## Making progress available outside the terminal

The update script writes a structured status file at `/var/lib/dragonwilds-control/status.env`. It records the operation, state, stage, percentage, message, timestamps, result, and paths to the backup and logs.

Writing to a temporary file and then renaming it gives readers a complete status record instead of exposing a file halfway through an update. Keeping stage and progress separate also gives the dashboard clearer information to present during long-running work.

The script retains the container output alongside its own explanatory messages. That preserves the evidence needed to investigate a missing progress update or a startup problem. A simplified dashboard message is useful day to day; the original output is what makes that message possible to verify later.

## How I validated the changes

I compared the earlier and revised scripts and confirmed that the change was confined to percentage handling. The backup procedure, container startup, recovery logic, and readiness checks remained the same.

The new patterns were checked against representative verification and download messages, including integer and decimal values. Isolated tests also identified their limits: the current patterns expect one whitespace character at each separator, and carriage-return-separated output can require additional handling.

I then checked the saved script directly on VM 200:

```bash
sudo bash -n /usr/local/sbin/dragonwildsCT-update \
  && echo 'Bash syntax OK'
```

The result was `Bash syntax OK`. This checked the saved file without performing maintenance. At this point, syntax validation and matching against captured output were complete; observing the revised progress reporting through a subsequent live update remained a separate check.

## Outcome and lessons

The project brought routine Dragonwilds management into Home Assistant and made the update procedure more explicit. The latest revision taught the script to recognize the SteamCMD progress format shown in the server logs.

The original SSH button was a useful first step because it made remote maintenance more convenient with very little complexity. Managing the server while away from home also made clear progress and results more valuable: I needed to know what the server was doing after I requested an action. Expanding the controls taught me to distinguish sending a command, completing a maintenance procedure, and confirming that the application is ready. Each needed its own evidence. As the controls took on more responsibility, the workflow needed a defined sequence, protection for persistent data, progress that reflected actual work, and a completion signal tied to the application.

Reviewing the script also exposed work still to do. Logging failures can interfere with recovery, and the background log follower needs explicit cleanup so it cannot retain the maintenance lock after the main script finishes. A failure to read logs can also be reported as a startup timeout because the follower's exit status is not collected. These issues were already present before the percentage change.

The recovery function attempts to bring the service back up, but it does not guarantee a rollback to the previous image or restore the saved world. Keeping that distinction clear helps me describe what the automation can actually recover from.

For future improvements, I want to test failure paths as deliberately as the successful path: unreadable logs, failed backups, interrupted monitoring, and restoration from an archive. Building these controls has been useful practice in Bash, log analysis, Docker administration, and documenting the evidence behind an operational decision.

[← Local Control, Segmentation, and Automation](evolution/09-local-control.md) · [HomeLab Portfolio](../README.md)
