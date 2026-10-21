# The notch prompt

The prompt I used to build my own notch on the Mac: music with live lyrics, weather, my messages, quick controls, and Claude Code asking for permission right from the notch. In White Matte and Dark Matte.

![The notch open in White Matte](notch-white.jpg)

![The notch open in Dark Matte](notch-dark.jpg)

1. The reference images are in this folder.
2. Copy the prompt below and paste it into Claude Code, on a Mac, with the two images attached.
3. Build it step by step: Claude shows you a plan first and waits for your OK.

**Prompt, for Claude Code**

````text
Build me a native macOS app (Swift + AppKit/SwiftUI, macOS 14 or later, Apple Silicon) that turns the area around the MacBook notch into a "Dynamic Island", like the iPhone one. It lives in the menu bar, has no Dock icon, and starts at login only if I turn it on.

I attached a screenshot of the notch I want: match its layout, sizes, spacing, rounded corners and colors as closely as you can, and use it to check each step.

Work in small steps. Before writing code, show me a short plan and the list of permissions the app will ask for, and wait for my OK. After every step, build it and tell me how to try it.

1. The island
- A borderless, transparent window that sits exactly over the notch and above all apps (also in full screen), centred on the screen that has the notch.
- States: resting (just the black notch), compact (a black pill that grows to the sides of the notch), peek (a small bubble under the notch for 2 to 4 seconds), expanded (opens 0.25 s after the mouse rests on the notch, closes when it leaves; a click keeps it open).
- Smooth spring animations, rounded corners that blend into the notch, a soft shadow.
- Two themes, flat and matte, no glass and no gradients, switchable from the menu:
  - Dark Matte: background #16181F, tiles #21242D, text #E3E7EF, secondary text #A4ABBA, accent #8FC7FF.
  - White Matte: background #F7F8FA, tiles #FBFBFC, text #1E2129, secondary text #545A69, accent #3B82D0.
  The black band of the real notch always stays black.

2. What's inside when it's open (each one a tile I can show, hide and reorder)
- Music: Spotify and Apple Music via AppleScript. Cover, title, artist, play/pause/next, a progress bar, and the current line of the lyrics, synced, from LRCLIB (free, no key), with a local cache.
- Weather from Open-Meteo (free, no key): temperature, icon, high and low, for a city I type in the settings.
- Next calendar event from EventKit.
- A focus timer (25 min) with start and reset.

3. Peeks (small bubbles that appear and go away)
- An app opens or quits (with its icon), charger connected, battery at 20% and 10%, Do Not Disturb on or off.

4. Claude Code, live in the notch
- Use Claude Code hooks (PreToolUse, Notification, Stop) that call a tiny script, which tells the app what Claude is doing (reading, editing, running a command, searching) through a local socket or a URL scheme.
- Compact state: an icon for the current step and a small animated grid while Claude works.
- When Claude asks for permission, open the island with the command and two buttons, Allow and Deny, plus two global shortcuts. Show the whole command, never a cut version, before I can approve it.
- When Claude finishes, show "Done" with how long it took.
- Give me the exact lines to add to ~/.claude/settings.json, and let me add them myself.

5. Settings
- A small menu in the menu bar: show or hide each tile, the city for the weather, Dark Matte or White Matte, launch at login, quit.

Things that will trip you up (handle them from the start)
- Find the notch with NSScreen.auxiliaryTopLeftArea / auxiliaryTopRightArea and safeAreaInsets.top; on Macs without a notch, draw a fake one at the top centre.
- The window needs a level above the menu bar and collectionBehavior [.canJoinAllSpaces, .fullScreenAuxiliary, .stationary], or it disappears in full screen and on other desktops. It must never steal focus (non-activating panel).
- Mouse tracking over the notch needs a tracking area on the panel, not on the menu bar.
- If you read Bluetooth state, add NSBluetoothAlwaysUsageDescription to Info.plist, or macOS kills the app.
- Do Not Disturb has no public API: use the Focus permission (INFocusStatusCenter) and say clearly when it isn't granted.
- Music: ask for the Automation permission once per player, and don't launch Spotify or Music if they're closed.
- Sign the app (even with an ad-hoc signature) and keep the same bundle id between builds, or macOS asks for permissions again every time.

Rules
- Privacy first: nothing leaves the Mac except the lyrics and weather requests. No analytics, no accounts.
- Ask for each permission only when the feature that needs it is first used (Automation for music, Calendar, Accessibility for shortcuts), and explain why in one line.
- Keep the code in a few clear files, with a README that says how to build, run and remove the app.
- If something can't be done on my macOS version, tell me and suggest the closest thing instead of faking it.
````

It won't come out identical on the first try. Mine is the result of weeks of small fixes. You'll get a working first version in an hour or two: then compare it with the image, tell Claude what's different, one detail at a time. Stuck? Write me on Instagram, I'll try to help.
