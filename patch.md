download the patched binary
```
wget -O uniond_patch https://github.com/unionlabs/union/releases/download/uniond%2Fv1.1.1-rc1.alpha1/uniond-release-x86_64-linux 
```
Stop uniond
```
systemctl stop union-testnet.service
```
Replace the binary with the new v1.1.1
```
mv ~/uniond_patch ~/.union/cosmovisor/current/bin/
```
Ensure it has proper permissions
```
chmod +x $DAEMON_HOME/cosmovisor/current/bin/uniond_patch
```
check the version
```
uniond_patch version
```
replace the current binary
```
mv uniond_patch uniond
```
Start your node
```
systemctl start union-testnet.service
```
check the logs
```
sudo journalctl -u union-testnet.service -f --no-hostname -o cat
```
