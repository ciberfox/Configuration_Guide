

1. Connect to the ESXi host: 
   Open an SSH client (such as PuTTY) and connect to the ESXi host using the IP address or hostname.

2. Enter maintenance mode: 
   Before upgrading, it's recommended to put the host into maintenance mode to ensure minimal disruption to running virtual machines. Run the following command to enter maintenance mode:
   ```
   esxcli system maintenanceMode set --enable true
   ```

3. Check the current version and available updates:
   Run the following command to check the current ESXi version and available updates:
   ```
   esxcli system version get
   esxcli software sources profile list --depot=<path_to_ESXi_offline_bundle>
   ```
   Replace `<path_to_ESXi_offline_bundle>` with the path to the ESXi offline bundle (.zip) file you want to upgrade to. You can download the latest offline bundle from the VMware website.

4. Stage the upgrade:
   Run the following command to stage the upgrade using the desired ESXi offline bundle:
   ```
   esxcli software profile update --depot=<path_to_ESXi_offline_bundle> --profile=<profile_name>
   ```
   Replace `<path_to_ESXi_offline_bundle>` with the path to the ESXi offline bundle file, and `<profile_name>` with the specific profile name for the upgrade. You can obtain the profile name from the output of the previous command. You can find URL here https://esxi-patches.v-front.de/

5. View the staged bulletins:
   To view the staged bulletins (upgrade details), run the following command:
   ```
   esxcli software sources profile get --depot=<path_to_ESXi_offline_bundle> --profile=<profile_name>
   ```

6. Start the upgrade:
   Once you are ready to start the upgrade, run the following command:
   ```
   esxcli system version install --source=<path_to_ESXi_offline_bundle> --profile=<profile_name> --reboot
   ```
   Replace `<path_to_ESXi_offline_bundle>` with the path to the ESXi offline bundle file, and `<profile_name>` with the specific profile name for the upgrade.

7. Monitor the upgrade progress:
   The upgrade process will begin, and you can monitor the progress. Once the upgrade is complete, the host will automatically reboot.

8. Exit maintenance mode:
   After the host has rebooted, you can exit maintenance mode by running the following command:
   ```
   esxcli system maintenanceMode set --enable false
   ```
