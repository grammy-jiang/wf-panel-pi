# Notification text alignment in wf-panel-pi 1.38

Evidence for the issue "Option to left-align notification text" in raspberrypi-ui/wf-panel-pi.

| File | What it shows |
| --- | --- |
| `problem-centred.png` | wf-panel-pi 1.38 from the Raspberry Pi archive. The red marks were added afterwards and show where each line starts. |
| `proposal-left-aligned.png` | A local build of the same 1.38 source package with `GTK_JUSTIFY_LEFT` and `gtk_label_set_xalign (GTK_LABEL (lbl), 0.0)` in `show_message()`. The red line was added afterwards and shows where every line starts. |
| `raw/` | The same two captures without marks. |
| `environment.txt` | Versions. |

The captures come from a headless labwc session with a private D-Bus session bus and the default Raspberry Pi desktop settings. The panel under test owns `org.freedesktop.Notifications`. Two notifications were sent, and grim took the screenshot 2.5 s later:

```sh
notify-send -i dialog-information "Backup complete" "Documents: 1,204 files
Pictures: 318 files
Next run: tomorrow at 02:00"
notify-send -i document-save "Download finished" "report-2026.pdf, 2.4 MB
Saved in Downloads"
```
