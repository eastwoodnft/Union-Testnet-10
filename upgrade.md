Union Testnet Upgrade Tutorial with Cosmovisor

This guide explains how to stage a software upgrade for the Union testnet (union-testnet-10) using Cosmovisor with the uniond binary version v1.1.0-rc1.alpha1. Cosmovisor automates the process of switching to a new binary during a chain upgrade, minimizing downtime.

Prerequisites

- Cosmovisor installed: Install Cosmovisor via:
  go install github.com/cosmos/cosmovisor/cmd/cosmovisor@latest
  or download the appropriate binary for your system.
- Node running: Ensure your node is running for union-testnet-10.
- Upgrade details: Confirm the upgrade name (assumed to be v1.1.0-rc1.alpha1) and block height from the Union testnet's governance proposal or documentation.
- System requirements: Linux system with wget, chmod, and basic utilities.

Steps to Stage the Upgrade

1. Download the New Binary

   Download the uniond binary for version v1.1.0-rc1.alpha1:
```
   wget https://github.com/unionlabs/union/releases/download/uniond%2Fv1.2.0-rc1alpha1/uniond-release-x86_64-linux -O uniond
```
   Make the binary executable:
```
   chmod +x uniond
```
2. Prepare the Upgrade Directory

   Create the directory structure for the upgrade in your node’s home directory (~/.union):
   ```
   mkdir -p ~/.union/cosmovisor/upgrades/v1.2.0/bin
   ```

   Note: Replace "v1.X.X-rc1.alpha1" with the exact upgrade name if it differs. Check the Union testnet governance proposal or documentation for the correct name.

4. Place the Binary

   Move the downloaded binary to the upgrade directory:
   ```
   mv uniond ~/.union/cosmovisor/upgrades/v1.2.0/bin/uniond
   ```

6. Verify the Binary

   Confirm the binary version:
   ```
   ~/.union/cosmovisor/upgrades/v1.2.0/bin/uniond version
   ```

   The output should show v1.1.0 or similar.

7. Monitor the Upgrade

   Check Cosmovisor logs to ensure the upgrade executes smoothly:
   ```
   journalctl -u cosmovisor -f
   ```

8. Post-Upgrade Verification

   After the upgrade, verify the node is running the new binary:
   ```
   uniond version
   ```

   Confirm the node is syncing and producing blocks:
   ```
   curl http://localhost:26657/status
   ```

   Check the latest_block_height and syncing fields in the output.

Additional Notes

- Backup: Always back up your node’s data directory (~/.union) before an upgrade to prevent data loss.
- Upgrade Name: Ensure the upgrade name (v1.1.0-rc1.alpha1) matches the name in the governance proposal exactly (case-sensitive).
- Testing: Test the upgrade process on a local or test environment if possible.
- Troubleshooting: If the upgrade fails, check Cosmovisor logs for errors. Common issues include incorrect binary paths, mismatched upgrade names, or missing dependencies.
- Resources: Refer to the Union testnet documentation (https://github.com/unionlabs/union) or governance proposals for chain-specific details.

For further assistance, contact the Union testnet community or check the latest governance proposals.
