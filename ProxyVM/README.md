# ProxyVM setup

### Automatically establish a VPN connection using NetworkManager on startup
Create a new Proxy VM and enable the `network-manager` service using Qube settings.
Create a new VPN connection using either `nmcli` or the NetworkManager applet in the system tray.

If the VPN connection is authenticated using TLS certificates, append the following to `/rw/config/rc.local`:
```
nmcli connection up my-vpn-connection
```
where `my-vpn-connection` is the connection name of NetworkManager.

Otherwise, if the authentication type is password-based, you will need to provide a username by editing
the connection using NetworkManager. A password entered using the applet will be stored in a keyring, which
isn't accessible for commands in the `rc.local` script.
For VPN connections that require credentials to authenticate, append the following contents to `/rw/config/rc.local`:
```
upVPN() {
  conname="$1"
  password="$2"
  passwd_path=$(mktemp)
  echo "vpn.secrets.password:$password" > "$passwd_path"
  nmcli connection up "$conname" passwd-file "$passwd_path"
}
upVPN my-vpn-connection mypassw0rd
```
Replace the last two arguments of the last line with the correct connection name and password, respectively.

