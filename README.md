# vmdynamicres

vmdynamicres is a script that automatically adjusts the optimal scaling for VMware virtual machines, when using them on different host machines.
This is especially useful when one uses the same VM on different hosts, with different Screen resolutions (e.g. Full HD and 4K).

## Prerequisites / Limitations

- The VM has to use X11 with GNOME Desktop environment
- Only one standard user actually uses the VM
- The mouse pointer is now captured within the VM - use Ctrl + Alt to get back to the host

## Installation

### Prepare GNOME Schema

You can also refer to [this tutorial](https://kaanlabs.com/ubuntu-set-scaling-factor-to-200-percent).

```
nano /usr/share/glib-2.0/schemas/90_hidpi.gschema.override

[org.gnome.desktop.interface]
scaling-factor=1

glib-compile-schemas /usr/share/glib-2.0/schemas

shutdown -r now
```

### Install vmdynamicres

```
sudo -i

cd /usr/local/bin
git clone <REPOSITORYADDRESS>
chown -R <youruser>:<youruser> vmdynamicres
chmod +x vmdynamicres/scaleSet125.sh vmdynamicres/scaleWatchdog.sh vmdynamicres/vmdynamicres.desktop vmdynamicres/xeventbind

nano vmdynamicres/vmdynamicres.desktop
Replace <YOUR-ROOT-PASSWORD> with your root password

cd /etc/xdg/autostart/
ln -s /usr/local/bin/vmdynamicres/vmdynamicres.desktop vmdynamicres.desktop

shutdown -r now
```

## License / Credits

vmdynamicres uses the [xeventbind utility written by ritave (Olaf Tomalka)](https://github.com/ritave/xeventbind), to automatically adjust for a changed VM window size.

vmdynamicres can be used under the MIT license.
