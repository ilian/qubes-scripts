# Dom0 setup

### Take screenshots
Copy the [screenshot-to-vm](screenshot-to-vm) script to dom0.
Running this script will prompt you to either click a window or draw a rectangular area to capture and
a target VM to copy the screenshot to. If the target has `xclip` installed, the screenshot will be
stored in the VM's clipboard. Otherwise, the screenshot is moved to `~/QubesIncoming/dom0/`.


If you run xfce in dom0, you can assign a hotkey such as print screen to this command using
`xfce4-keyboard-settings`.

### Monitor CPU usage across all VMs
The following command will show the average CPU utilization of a 1 second sample across all Xen domains:
```
sh -c "xentop -b -d 1 -i 2 | awk 'NR > 1 { s += \$4 } END { printf \"%.1f%\", s }'"
```
This can be continuously monitored by dom0 using the "Generic Monitor" Xfce panel plugin.
Make sure to configure the plugin's period greater than the configured sample interval to avoid freezes.

