Arkitexe ServerFeel
===================

A Halo Infinite capture-and-log agent. It watches Halo's game traffic,
works out which Azure server hosted each match, measures your real ping
to it, and logs every match so "this match felt off" can be checked
against numbers later.

It never touches the game, never modifies traffic and never talks to
343/Microsoft on your behalf. It only listens.


HOW TO RUN
----------
1. Unzip this folder anywhere (Desktop is fine). Keep the folder intact -
   ServerFeel.exe needs the _internal\ folder next to it.
2. Double-click ServerFeel.exe.
3. Accept the Windows admin (UAC) prompt. Packet capture uses the WinDivert
   kernel driver, which requires administrator rights. There is no way
   around this.
4. If Windows SmartScreen says "Windows protected your PC": click
   "More info" then "Run anyway". The exe is not code-signed.
5. Start Halo. Matches are detected and logged automatically. Hover the
   SESSION WATCHER bubble to see the live server, region and ping.

To quit: the QUIT bubble or the window's X. The tray icon's "Hide" only
minimizes it - the app keeps running and capturing.


REQUIREMENTS
------------
- Windows 10 or 11, 64-bit.
- Microsoft Edge WebView2 runtime. Windows 11 ships it. If ServerFeel
  says it is missing, run MicrosoftEdgeWebview2Setup.exe from this folder
  once and launch again.
- Internet on first launch: it downloads Microsoft's Azure IP-range list
  (a few MB) so servers can be mapped to regions. Cached afterwards.


WHERE YOUR DATA GOES
--------------------
Everything lands under your own profile, nothing in this folder:

    %USERPROFILE%\Arkitexe\serverfeel\
        feel.db          every match + ping measurements (SQLite)
        sessions\        per-session .log and .jsonl
        matches\         one plain-text summary per match
        crash.log        only exists if something went wrong - send this
        trace.log        program trace, useful with crash.log

Delete that folder to reset.


THINGS TO KNOW
--------------
- Do NOT run clumsy (the network-condition simulator) at the same time.
  Both use the WinDivert driver and clumsy's registration breaks
  ServerFeel's capture until you reboot.
- Some antivirus products flag WinDivert64.sys because it is a packet
  filter driver. It is the standard, signed WinDivert 2.2 driver used by
  many networking tools.
- The "measured ping" shown is a 1 Hz ICMP probe to the elected game
  server. The path-health "est. loss" figure is an estimate from stream
  regularity, not measured packet loss.
- Halo's Easy Anti-Cheat has coexisted with this capture method across
  thousands of matches. Capture is read-only (SNIFF mode).
