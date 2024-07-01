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
![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/4d2f387c-e43c-4c73-b6ec-d91cf7d51c5b/40b76799-44c4-4e24-bcd2-0a2737ca8e9a/Untitled.png)
2. Let's install the wget and curl tools:

  ```
   sudo apt install wget curl
  ```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/4d2f387c-e43c-4c73-b6ec-d91cf7d51c5b/fff82639-5069-4ac0-8cdb-a09d07835f83/Untitled.png)
3. Let's install Rust:

  ```
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs/ | sh
  ```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/4d2f387c-e43c-4c73-b6ec-d91cf7d51c5b/74371a41-c692-43cf-98f5-485d298b654f/Untitled.png)
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
https://prod-files-secure.s3.us-west-2.amazonaws.com/4d2f387c-e43c-4c73-b6ec-d91cf7d51c5b/742f99c9-a08d-4c46-ba0f-0d897e540d9d/Untitled.png
7. ``source /root/.bashrc``
8. Let's check the Fuel version:
  ```
  fuelup --version
  ```
1. Let's check the toolchain version:

```bash
fuelup show
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/4d2f387c-e43c-4c73-b6ec-d91cf7d51c5b/ffa940e8-fd2e-477c-afe8-6c59064e5f7e/Untitled.png)

1. Create a new P2P key pair:

````bash
fuel-core-keygen new --key-type peering
```

A window with keys will open, you need to save the keys. Highlight the entire contents of the opened window, copy it via CTRL+C and transfer it to notepad. The previously opened window will close.
