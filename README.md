# My Kinda-WSL setup 🎃

## VirtualBox and Ubuntu 🪟

1. Download and install VirtualBox on Windows from the official website including all optional packages and requirements ([link](https://www.virtualbox.org/wiki/Downloads))

1. Download Ubuntu image from the official website ([link](https://ubuntu.com/download/desktop))

1. Create a VM and install Ubuntu with

    - Skipping unattended installs

    - 4 cores

    - 4096 MB of RAM

    - 25 GB of VHD

    - Guest additions

1. Make sure you enable audio input from the bottom bar

## SSH 🍪

1. Enable SSH in Ubuntu with

    ```sh
    sudo apt install openssh-server
    sudo systemctl enable ssh --now
    sudo ufw allow ssh
    sudo ufw enable
    ```

1. Create a port forwarding rule 22->2222 in VirtualBox. There's no need to set the IP addresses.

1. Generate and set the SSH key in Windows

    ```batch
    ssh-keygen
    cat ~/.ssh/id_rsa.pub | ssh enrico@localhost 'cat >> .ssh/authorized_keys'
    ```

1. Fix the time in Ubuntu

    ```bash
    sudo hwclock --hctosys 
    ```

1. Install ZSH and OhMyZsh in Ubuntu

    ```bash
    sudo apt update
    sudo apt install git zsh
    zsh
    chsh -s $(which zsh)
    sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
    ```

1. Force the display in SSH, add `export DISPLAY=:0` to `~/.zshrc`

## Terminal profile 📒

1. Create a batch script with the following content and save it somewhere

    ```batch
    @echo off
    & 'C:\Program Files\Oracle\VirtualBox\VBoxManage.exe' list runningvms | find "Ubuntu" > nul
    if not errorlevel 1 (
      & 'C:\Program Files\Oracle\VirtualBox\VBoxManage.exe' startvm "Ubuntu" --type headless
    )
    ssh -p 2222 enrico@localhost
    ```

1. Create a new profile in the terminal app and select the batch script

## Visual Studio Code 🎙️

1. Install the `Remote - SSH` extension in Visual Studio Code

1. Select `Connect to host`, then `Add new Host` and insert `ssh -p 2222 enrico@enrico-ubuntu`

1. Select `Connect to host`and then `enrico-ubuntu`