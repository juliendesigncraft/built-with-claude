# Pulsar Lite

Pulsar is the app that lives in my Mac's menu bar. Pulsar Lite is the free part of it: a clean menu bar, your desktop in a menu, a sound for every key, and the small system switches in one place.

This folder is the prompt to build your own Pulsar Lite with Claude Code. You get the code, it's yours, and you can change anything.

## How to use it

1. Copy the prompt below.
2. Paste it into Claude Code, on a Mac, in an empty folder.
3. Build it step by step: Claude shows you a plan first and waits for your OK.

**Prompt, for Claude Code**

````text
Build me a native macOS app (Swift + AppKit, macOS 14 or later) called Pulsar Lite. It lives in the menu bar, has no Dock icon, and starts at login only if I turn it on. No Xcode project: one build.sh that compiles with swiftc and makes the .app.

Work in small steps. Before writing code, show me a short plan and wait for my OK. After every step, build it and tell me how to try it.

1. A clean menu bar
- Pulsar is a small capsule in the menu bar. Left click opens the menu. Right click (or Option click) shows or hides all the hidden icons at once.
- "Clean menu bar" hides every icon to the left of the capsule. I choose what to hide by Command-dragging icons to the left of it. Remember the state between launches.
- "Background apps (n)": every app that lives only in the menu bar (no Dock icon), with its real icon and name, even when there is no room for its icon. Click one to bring it forward. Leave out Apple's own apps.

2. My desktop in a menu
- "Desktop (n)": the folders and files on my Desktop as menu items with their real Finder icons, so colored folders stay recognizable. Folders first, then files, alphabetical.
- Show 5 at the first level and put the rest in "More n...", a submenu that holds all of them, not only the extra ones. Let me choose 4, 5, 6 or 8.
- Nothing is ever moved or changed: it's a list of shortcuts that reads ~/Desktop.

3. A sound for every key
- A sound on every key press and click, in every app.
- Sound packs: a few mechanical keyboards, each with its own space, return and delete, plus the key release. And a typewriter, with a bell on the 62nd key of the line, like reaching the margin.
- The mouse clicks too, with its own sound.
- Two volume sliders, Keyboard and Mouse. When I release a slider, play one key at the new volume.
- Find sound packs under an open license (MIT or CC0) and keep a SOUNDS.md with where each one comes from and its license. Never use sounds from a paid app.

4. The small switches
- Toggles: Dark Mode, Hide desktop icons, Show hidden files, Keep awake, Mute, Stage Manager, Do Not Disturb.
- Actions: Screen saver, Lock screen, Empty Trash (it asks first).

Style
- Dark always, menus and windows, whatever the system theme. Dark #1D1F29, cards #252836, one accent blue #8FC7FF. No borders, no outlines. One typeface only, SF.

Things that will trip you up
- Clean menu bar is the Hidden Bar trick: an invisible status item to the left of the capsule grows to 10,000 pt, and macOS hides whatever doesn't fit.
- On first launch macOS puts a new status item to the left of all the others, so nothing would be hidden. Set a starting position next to the system icons with the "NSStatusItem Preferred Position" defaults key for your items.
- On macOS 26 the status items are hosted by Control Center. If the capsule doesn't show up after a restart, killall ControlCenter and open the app again. Write that in the README.
- Key sounds in other apps need the Accessibility permission. Clicks work without it.
- Sign every build with the same local code signing certificate, not ad hoc. With ad hoc signing macOS ties the permission to the file's fingerprint and every rebuild loses Accessibility.
- Never call AVAudioPlayerNode.play() on the main thread: with a stuck CoreAudio it can wait forever and freeze the whole app. Play sounds on their own queue, keep the voices running, let a new hit interrupt the old one, and drop new hits when more than 4 are waiting.
- When the audio output changes (AirPods, headphones) macOS stops the audio engine. Listen for AVAudioEngineConfigurationChange, reconnect and restart.
- Short clicks sound quiet under music. Give each sound a soft saturation when it loads (tanh, drive 2, peak 0.9) instead of raising the peak.
- Vary the volume of each hit a little, and let up to 12 sounds overlap, so fast typing doesn't cut the tails.
- Dark Mode: AppleScript to System Events (macOS asks for Automation the first time). Hide desktop icons and Show hidden files: defaults write com.apple.finder (CreateDesktop, AppleShowAllFiles), then restart Finder. Keep awake: start and stop caffeinate -di. Stage Manager: defaults com.apple.WindowManager GloballyEnabled.
- Apple has no public API for Focus. Do Not Disturb runs a shortcut I create once in the Shortcuts app, called "Pulsar DND", with the "Set Focus" action.

Rules
- Nothing leaves the Mac. No accounts, no analytics, no network.
- A README that says how to build, run and remove the app.
````

It won't come out identical to mine on the first try. You'll get a working first version in a session or two: then use it every day and ask Claude for one detail at a time.

## Want the rest of Pulsar?

My full Pulsar does more: Claude Code live in the notch (permissions, questions, sessions), a volume dial with a mixer for each app, the island with music and live lyrics, Stow, Rowline and the Dark and White Matte themes. Those parts are sold as a ready app on Gumroad: Pulsar Agent, Pulsar Mixer and Pulsar Complete. [juliendesigncraft.gumroad.com](https://juliendesigncraft.gumroad.com)
