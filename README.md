# FuelNode

## This guide will detail the installation of a node in the Fuel project.

Server requirements(recommended):

- CPU: 8 cores;
- RAM: 12 GB;
- Storage: 100 GB SSD
- OS: Ubuntu 22.04

**I rented a PARs-3 server on Aeza for this node for 20 euros/month. It will be fine as well.**
1. Let's update the packages:

  ```
  sudo apt-get update && sudo apt-get upgrade -y
  ```

2. Let's install the wget and curl tools:

  ```
   sudo apt install wget curl
  ```


3. Let's install Rust:

  ```
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs/ | sh
  ```


4. Customize the current shell:

  ```
  . "$HOME/.cargo/env"
  ```

5. Check the version of Rust:

  ```
  rustup --version
  ```

6. Install Fuel toolchain. During the installation process, press "y" to confirm the installation:

  ```
  curl https://install.fuel.network | sh
  ```

7. ``source /root/.bashrc``
8. Let's check the Fuel version:
  ```
  fuelup --version
  ```
9. Let's check the toolchain version:

  ```
  fuelup show
  ```


10. Create a new P2P key pair:

  ```bash
  fuel-core-keygen new --key-type peering
  ```

A window with keys will open, you need to save the keys. Highlight the entire contents of the opened window, copy it via CTRL+C and transfer it to notepad. The previously opened window will close.
11. Create a "fuel" folder:

  ```
  mkdir fuel
  ```

12. Let's move to "fuel":

  ```
  cd fuel
  ```

13. Download the official configuration file to run the node:

  ```bash
  wget https://raw.githubusercontent.com/FuelLabs/fuel-core/v0.22.0/deployment/scripts/chainspec/beta_chainspec.json
  ```
14. Go to [Alchemy](https://alchemy.com/?r=TM5MTAyNzUxNDcyM), create a new App, open "API key" and copy the HTTPS link:
15. Create a service file for the node to run in the background:
**Replace the following parameters with their own values:**
<NODE_NAME> for any node name;
<P2P_SECRET> to the secret key from step 10, we copied it;
<SepoliaETH_RPC_ENDPOINT> to the copied HTTPS link from Alchemy.

```
echo "[Unit]
Description=Fuel Node Beta-5
After=network.target

[Service]
User=root
Type=simple
ExecStart=/root/.fuelup/toolchains/latest-x86_64-unknown-linux-gnu/bin/fuel-core run \
--service-name=<NODE_NAME>-sepolia-testnet-node.
--keypair <P2P_SECRET> \.
--relayer <SepoliaETH_RPC_ENDPOINT> \.
--ip=0.0.0.0.0 --port=4000 --peering-port=30333.
--db-path ~/.fuel_beta5.
--utxo-validation --poa-instant false --enable-p2p.
--reserved-nodes /dns4/p2p-testnet.fuel.network/tcp/30333/p2p/16Uiu2HAmDxoChB7AheKNvCVpD4PHJwuDGn8rifMBEHmEynGHvHrf\
---sync-header-batch-size 100 --
--enable-relayer
--relayer-v2-listening-contracts 0x557c5cE22F877d975C2cB13D0a961a182d740fD5 \
--relayer-da-deploy-height 4867877.
--relayer-log-page-size 2000
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/fueld.service
```

I attach my service file for an example:
```
echo "[Unit]
Description=Fuel Unit Beta-5
After=network.target

[Service]
User=root
Type=simple
ExecStart=/root/.fuelup/toolchains/latest-x86_64-unknown-linux-gnu/bin/fuel-core run \
--service-name=M0zgiiiNode-sepolia-testnet-node \.
--keypair 4d57fd73aee2332852b3df145a3147e04d6e2d07150d7351d549338629802a6a \
--relayer https://eth-sepolia.g.alchemy.com/v2/GKKM_TZbSOgjZ_VBCcmRKzYlRO0KVGbj \
--ip=0.0.0.0.0 --port=4000 --peering-port=30333.
---db-path ~/.fuel_beta5 --
--utxo-validation --poa-instant false --enable-p2p.
--reserved-nodes /dns4/p2p-testnet.fuel.network/tcp/30333/p2p/16Uiu2HAmDxoChB7AheKNvCVpD4PHJwuDGn8rifMBEHmEynGHvHrf\
--sync-header-batch-size 100 \\\\
--enable-relayer
--relayer-v2-listening-contracts 0x557c5cE22F877d975C2cB13D0a961a182d740fD5 \
--relayer-da-deploy-height 4867877.
--relayer-log-page-size 2000
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/fueld.service
```
After substituting your own values, paste this command into the server window and press Enter.

17. Let's perform a daemon reload:
    
  ```
  systemctl daemon-reload
  ```

19. Enable the node service:
  ```
  systemctl enable fueld
  ```
20. Start the node service:

  ```
  systemctl start fueld
  ```
22. Check the status of fueld.service:
  ```    
  systemctl status fueld.service
  ```
1. Lastly, let's check the logs:

  ```
  journalctl -u fueld -f -o cat
  ```

**Alchemy will start displaying queries**

**At this point, the installation of the Fuel node has come to an end.**

## A list of useful commands is provided below:
1. Stopping the node service file:

  ```
systemctl stop fueld
  ```

2. Deleting the node service file:
   
  ```
   rm /etc/systemd/system/fueld.service
  ```

3. Deleting node folders:

   
  ```
  rm -rf fuel 
  rm -rf .fuelup 
  rm -rf .forc 
  rm -rf .fuel_beta5
  ```

4. Checking the logs:

  ```
  journalctl -u fueld -f -o cat
  ```

5. ```fuel-core run --help```


