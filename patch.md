download the patched binary
```
wget -O https://github.com/unionlabs/union/releases/download/uniond%2Fv1.1.1-rc1.alpha1/uniond-release-x86_64-linux uniond_patch
```
Stop uniond
```
systemctl stop union=testnet.service
```
Replace the binary with the new v1.1.1
```
cp ~/uniond_patch ~/.union/cosmovisor/current/bin/
```
Ensure it has proper permissions
```
chmod +x $DAEMON_HOME/cosmovisor/current/bin/$DAEMON_NAM
```
Start your node
```
systemctl start union-testnet.service
```
check the logs
```
sudo journalctl -u union-testnet.service -f --no-hostname -o cat
```
