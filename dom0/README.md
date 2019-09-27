# Dom0 setup

### Monitor CPU usage across all VMs
The following command will show the average CPU utilization of a 1 second sample across all Xen domains:
```
sh -c "xentop -b -d 1 -i 2 | awk 'NR > 1 { s += \$4 } END { printf \"%.1f%\", s }'"
```
This can be continiously monitored by dom0 using the "Generic Monitor" Xfce panel plugin.
Make sure to configure the plugin's period greater than the configured sample interval to avoid freezes.
