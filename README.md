# Evidence: wf-panel-pi crashes when a queued notification is replaced

Captured on Raspberry Pi OS trixie (Raspberry Pi 5, labwc 0.20.1) on an isolated headless labwc session with a private session bus, panel running under gdb. Each directory holds:

- `session.log`: the exact `notify-send` commands, their output and the panel's bus state after each step
- `1-before-replace.png`, `2-after-replace.png`: screenshots of the test output before and after the replace
- `before-after.png`: the top-right corner of both screenshots side by side with captions (not in `unstripped-1.34`)
- `panel-stderr-and-backtrace.log`: GTK criticals from the panel's stderr and the gdb backtrace (if it crashed)
- `gdb.log`: raw gdb session output
- `environment.txt`: binary provenance and package versions

| directory | binary | scenario | result |
| --- | --- | --- | --- |
| `stock-1.34` | archive `wf-panel-pi_1.34_arm64.deb`, unmodified | replace a notification queued behind another one | SIGSEGV |
| `stock-1.34-startup-mute` | same | replace a notification posted during the 2.5 s start-up mute | SIGSEGV |
| `unstripped-1.34` | 1.34 rebuilt from the archive source with `nostrip`, unmodified | queued replace | SIGSEGV, symbolized backtrace |
| `patched-1.34` | 1.34 rebuilt with the proposed fix | queued replace | panel alive, notification shown with the updated text |
| `patched-1.34-startup-mute` | same | start-up mute replace | panel alive, notification shown with the updated text |
