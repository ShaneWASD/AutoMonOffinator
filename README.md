<img width="2559" height="1439" alt="6" src="https://github.com/user-attachments/assets/a96e2b91-cf54-4cf2-b4c2-2817c50c8d2b" />
# AutoMonOffinator

**OLED Care Tool – Prevent Screen Burn-in**

AutoMonOffinator is a lightweight Windows utility designed to protect OLED screens from burn-in by automatically dimming static interface elements. It intelligently detects idle states, video playback, and UI activity to reduce pixel wear without sacrificing usability.

## Features

- **Taskbar Dimmer** – dims the Windows taskbar when not in use  
- **Browser UI Dimmer** – darkens browser edges (top/sides) while keeping content visible  
- **Screen Dimmer** – dims the entire screen after idle timeout; features *Focus Dimming* that leaves video areas un-dimmed  
- **App UI Dimmer** – dims any application window using custom layer profiles (margins, multiple layers)  
- **System Tray Icon** – quick access to settings and exit  
- **Watchdog** – automatically restarts crashed components  
- **Multilingual** – interface language adapts to system locale (Russian/English)  
- **Resource-Friendly** – runs as a single process with native WinAPI overlays (no Tkinter)

## System Requirements

- Windows 10 / 11 (64-bit)  
- No additional runtime installations required

## Installation

1. Download the latest release from the [Releases](../../releases) page  
2. Extract the ZIP archive to any folder  
3. Run `AutoMonOffinator.exe`

The program runs in the background – check the system tray for the icon.

## Usage

### Tray Icon Menu

Right‑click the tray icon to access:

- **Settings...** – opens the configuration console  
- **Donate to author** – support the developer  
- **Exit** – closes the application

### Configuration Console

<img width="739" height="615" alt="1" src="https://github.com/user-attachments/assets/6513def3-d557-4db8-bb38-d0398edf83e7" />


The console provides full control over all dimming modules and system power settings.

#### Basic Parameters

<img width="736" height="606" alt="2" src="https://github.com/user-attachments/assets/4f980908-de88-4c45-93c1-f6ccd774207a" />


- **Idle timeout** – time of user inactivity (keyboard, mouse, gamepad) before dimming or monitor turn‑off.  
- **Check video in browsers** – enables video detection in visible browser windows to prevent dimming while content is playing.  
- **Min changed pixels** – sensitivity for video motion detection (lower = more sensitive).  
- **Static image timeout** – if a full‑screen window shows no changes for this period, the monitor turns off.  
- **Similarity threshold (SSIM)** – how similar two consecutive screenshots must be to consider the image “static”.  
- **Check interval** – how often the static‑image check runs.  
- **Timeout after monitor off** – delay before entering sleep/hibernate after the screen turns off.  
- **Mode after monitor off** – choose between Sleep or Hibernate.  
- **Auto‑restart crashed dimmers** – watchdog that respawns any dimmer process if it fails.  
- **Autostart with system** – adds the program to Windows startup.  
- **Excluded processes** – list of processes that prevent monitor turn‑off (e.g., video players).

#### Dimmer Modules

**Taskbar Dimmer**  
- Enable/disable, dimming strength (0–100%), width percentage (portion of taskbar to dim), fade‑in/out speeds.

<img width="731" height="614" alt="3" src="https://github.com/user-attachments/assets/34efe7bc-de1e-479d-af28-12f2acc56af7" />


**Browser UI Dimmer**  
- Enable/disable, dimming strength, fade speeds, edge margins (top, bottom, left, right in pixels), and a list of browser processes to exclude.

<img width="701" height="615" alt="4" src="https://github.com/user-attachments/assets/7423ca66-299a-4f47-878e-99b0762be69e" />


**Screen Dimmer** (idle dimming)  
- Enable/disable, dimming strength, idle timeout (in minutes), fade speeds, and option to check video in browsers.  
- **Focus Dimming** – when enabled, the screen dimmer creates a “hole” around the video area on the monitor, so the video remains at full brightness while the rest of the screen is dimmed. Settings:  
  - Focus check interval – how often the system searches for video regions.  
  - Min video area – minimum size (in pixels) of the video rectangle to activate focus dimming.  
- **Ignored monitors** – list of monitors where screen dimming is disabled.  
- **Additional video processes** – extra process names that should be treated as video sources (e.g., custom media players).  
- **Excluded processes** – processes that prevent screen dimming from activating.

<img width="737" height="614" alt="5" src="https://github.com/user-attachments/assets/ba024795-1432-4bdb-8af0-2c65ef14ffcf" />


**App UI Dimmer**  
- Enable/disable, and manage **profiles** for individual applications.  
- Each profile defines a process name, dimming strength, fade speeds, and **layers**.  
- A layer consists of margins (top, bottom, left, right) that create dimmed bands around the window. Multiple layers can be stacked, and hovering over any layer makes it transparent together with all higher layers – perfect for toolbars or side panels.

<img width="651" height="588" alt="7" src="https://github.com/user-attachments/assets/a08b1aa1-4a13-4dfe-b846-b235ab7438f5" />


#### Additional Actions

- **Delete / Restore hibernation file** – manage `hiberfil.sys`.  
- **Reset Windows sleep timers** – set sleep timeout to “Never”.  
- **Reset Windows hibernate timers** – set hibernate timeout to “Never”.  
- **Reset monitor turn‑off** – set display turn‑off to “Never”.

All settings are saved to `AutoMonOffinatorResources/AutoMonOffinator_config.json` and take effect within a few seconds.

### How It Works

- The **ScreenSaverMonitor** continuously tracks user input (keyboard, mouse, gamepad).  
- When idle time exceeds the threshold, it checks for video playback in visible browser windows using frame‑by‑frame motion analysis.  
- If no video is detected, it either dims the screen or turns the monitor off (depending on settings).  
- The **Focus Dimming** subsystem periodically captures the screen to locate video rectangles and applies a dynamic overlay that leaves only the video area visible.  
- All other dimmers (taskbar, browser UI, app UI) run independently, each monitoring window geometry and applying overlays with smooth fade animations.

## License

This software is provided free of charge for personal and commercial use. Redistribution, modification, or reverse engineering is strictly prohibited without explicit permission from the author.

## Donations

If you find this tool useful and want to support its development, please consider a donation:

[Donate via Boosty](https://boosty.to/shanewasd/donate)

Your support helps keep the project alive and updated.
