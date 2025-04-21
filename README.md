<p align="center">
<img src="https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white"><img src="https://badges.frapsoft.com/os/v2/open-source-175x29.png?v=103"><br><a href="https://www.kernel.org/category/about.html"><img src="https://badges.frapsoft.com/bash/v1/bash-200x34.png?v=103"><a href=""></a>

<br>
	
<h1 align="center"><b><i>Simple, important & cool resources for</b></i></h1>
<h3 align="center">(Ubuntu)</h3>
<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Linux_Mint_Logo_%28until_2021%29.svg/1200px-Linux_Mint_Logo_%28until_2021%29.svg.png?20210414163034" width=50%></p>

To Do 
- [ ] Replace Ananicy with <a href="https://github.com/AdnanHodzic/auto-cpufreq"><b>auto-cpufreq</b></a>
- [ ] Add <a href="https://waydro.id/index.html"><b>Waydroid</b></a>
- [ ] Add <a href="https://github.com/wwmm/easyeffects"><b>EasyEffects</b></a> for PipeWire's audio server only
- [ ] Add <a href="https://www.qemu.org/"><b>QEMU</b></a>
- [ ] Add <a href="https://gitlab.com/volian/nala#nala"><b>Nala</b></a> package manager

# Contents
Please check the original repository at https://github.com/trinib/Awesome-Mint-Setup for the full content.

***

<h2 align="center">🔧<b><i>CUSTOM KERNELS & DRIVERS</b></i>🔧</h2>

> [!NOTE]
<i>Depending on the type of hardware you have, one **might** work better than the other. But in my opinion XanMod good for gaming and Liquorix for heavy tasks like video editing, vscode etc.</i>

#### <a href="https://xanmod.org/"><b>XanMod</b></a>

    echo 'deb http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list
    wget -qO - https://dl.xanmod.org/gpg.key | sudo apt-key --keyring /etc/apt/trusted.gpg.d/xanmod-kernel.gpg add -
    sudo apt update && sudo apt install linux-xanmod
      
or

#### <a href="https://liquorix.net/"><b>Liquorix</b></a>

    sudo add-apt-repository ppa:damentz/liquorix && sudo apt-get update
    sudo apt-get install linux-image-liquorix-amd64 linux-headers-liquorix-amd64
    sudo reboot
	
***
**[⬆ BACK TO TOP ⬆](#contents)**
	
<h2 align="center"><b><i>🔊BOOST AUDIO🔊</b></i> </h2>

###  Equalizer 

<a href="https://flathub.org/apps/details/com.github.wwmm.pulseeffects"><b>Pulse Effects</b></a> (will make soft speakers alot louder)
	
<img src="https://user-images.githubusercontent.com/18756975/168470285-7d16cddc-38ca-4ac3-8829-69cc6bf17297.png" width=350px height=200px><br>
```
sudo apt-get install pulseeffects lsp-plugins
````

Presets
> <a href="https://github.com/JackHack96/EasyEffects-Presets/tree/pulseeffects"><b>pulse-presets</b></a>


###  Audio Tweaks 
Check out this <a href="https://github.com/trinib/Awesome-Linux-Mint-Basics/blob/main/Enable%20High%20Quality%20Audio.md"><b>guide</b></a>

###  Troubleshoot 
If there is any issue with your audio like *_lag_* or in my case *_louder volume_* feature was not working, From linux-mint forums :
```
killall pulseaudio
sudo killall pulseaudio
sudo apt-get purge pulseaudio pulseaudio-utils gstreamer0.10-pulseaudio libpulse-browse0 paman pavumeter pavucontrol
sudo mv /etc/asound.conf /etc/asound.conf-bak
rm ~/.pulse-cookie
rm -r ~/.pulse
sudo apt-get install libalsaplayer0
```
	
***
**[⬆ BACK TO TOP ⬆](#contents)**

<h2 align="center">🔋<b><i>BETTER BATTERY</b></i>🔋</h2>

###  Install <a href="https://linrunner.de/tlp/"><b>TLP</b></a> package 
1. Open synaptic package manager
2. Search for tlp package
3. Right click package, select mark for installation and mark
4. Click apply
	
###  Disable Bluetooth 
```	
sudo systemctl disable bluetooth.service    
## To re-enable
sudo systemctl enable bluetooth.service
```
###  Turn Off Firewall Logs 
```
sudo ufw logging off 
## To re-enable
sudo ufw logging low
```	
###  Disable Gome features 

Disabling Vsync&Windows Compositing (found in `general`)
	
Disable Startup Apps
	
Disable All Effects & Animations
	
Disable Automatic Screen Rotation (found in `display settings`)

***
**[⬆ BACK TO TOP ⬆](#contents)**

<h2 align="center">🚀<b><i>OPTIMIZE RAM&SSD</b></i>🚀</h2>

###  Decrease <a href="https://www.linux.com/news/all-about-linux-swap-space/"><b>swap</b></a> 

_Only if using 8gb ram or more for less disk writes and more use of memory_
	
Open:
```
sudo nano /etc/sysctl.conf
````
Add at end of file :

`vm.swappiness = 10`
	
<i>This means when 10% of ram is only available, swap will activate</i>
	
###  Set VFS cache pressure 
	
<i>VFS cache pressure pushes the kernel to return memory being used for caching to the main pool of free memory</i>
	
Open:
```
sudo nano /etc/sysctl.conf
````

Add at end of sysctl.conf file:
	
`vm.vfs_cache_pressure=50`


###  Disables write access 
	
<i>Noatime mount option fully disables writing file access times to SSD every time you read a file, this reduces the writes to SSD therefore greatly increasing lifespan of SSD's</i>
```
sudo nano /etc/fstab
```
<p align="center">
 <img src="https://i.imgur.com/pM1Mf4C.png" width=400px height=200px>	
	
###  Prevent out of memory 

> [!CAUTION]
> This tool is outdated and has not been updated for a while. If have issues try <a href="https://github.com/rfjakob/earlyoom"><b>earlyoom</b></a> or <a href="https://github.com/facebookincubator/oomd"><b>oomd</b></a>
	
Install <a href="https://github.com/hakavlad/nohang"><b>Nohang</b></a>:
```  
sudo add-apt-repository ppa:oibaf/test
sudo apt update
sudo apt install nohang
sudo systemctl enable --now nohang-desktop.service
```

***
**[⬆ BACK TO TOP ⬆](#contents)**

<h2 align="center">💻<b><i>BETTER CPU</b></i>💻</h2>
	
> [!WARNING]
> This tool is outdated and has not been updated for a while. Please use <a href="https://github.com/AdnanHodzic/auto-cpufreq"><b>auto-cpufreq</b></a>. Have not have time to use it and write quick tutorial.

###  Manage processes IO and CPU priorities with <a href="https://github.com/Nefelim4ag/Ananicy"><b>Ananicy</b></a> 
```
git clone https://github.com/Nefelim4ag/Ananicy.git /tmp/ananicy
cd /tmp/ananicy
sudo make install
sudo systemctl enable ananicy
sudo systemctl start ananicy
```
	
***
**[⬆ BACK TO TOP ⬆](#contents)**

<h2 align="center">🖱️<b><i>TOUCHPAD GESTURES</b></i>🖱️</h2>

###  Install <a href="https://github.com/JoseExposito/touchegg"><b>Touchegg</b></a> 
```
sudo add-apt-repository ppa:touchegg/stable
sudo apt update
sudo apt install touchegg
sudo systemctl enable touchegg.service
sudo systemctl start touchegg
mkdir -p ~/.config/touchegg && cp -n /usr/share/touchegg/touchegg.conf ~/.config/touchegg/touchegg.conf
```

Install <a href="https://github.com/JoseExposito/touche"><b>Touché</b></a> application in software manager to configure gestures 

or

Do it <a href="https://github.com/JoseExposito/touchegg#available-gestures"><b>maunally</b></a> from config file
```
sudo nano ~/.config/touchegg/touchegg.conf
```
<i>Here is my <a href="https://github.com/trinib/Awesome-Basic-Linux-Mint/blob/main/Touchegg_Settings.txt"><b>configuration</b></a> for reference</i>

***
**[⬆ BACK TO TOP ⬆](#contents)**

<h2 align="center">🎨<b><i>CUSTOMIZATION</b></i>🎨</h2>

<h3 align="center"><b><i>𝕐𝕌𝕄 ℂ𝔸ℕ𝔻𝕐</b></i> </h3>
<p align="center">
 <img src="https://i.imgur.com/E8S35nT.png" width=400px height=200px>	
	
###  All themes example here are from <a href="https://www.pling.com/s/Gnome/browse"><b>Pling</b></a> website.

#### <a href="https://www.pling.com/p/1445634/#files-panel"><b>Rainbow cursor</b></a>

Extract zip files to `/usr/share/icons/ `

#### <a href="https://www.gnome-look.org/p/1253385/"><b>Sweet dark ui theme</b></a>

Extract zip files to `/usr/share/themes/ `

#### <a href="https://www.cinnamon-look.org/p/1425426"><b>Beautyline icon theme</b></a>
Extract zip files to `/usr/share/icons/`
	
###  Applets 
	
#### <a href="https://cinnamon-spices.linuxmint.com/applets/view/281"><b>CinnVIIStarkMenu</b></a>
#### <a href="https://cinnamon-spices.linuxmint.com/applets/view/106"><b>CPU Temp Indicator</b></a>
#### <a href="https://cinnamon-spices.linuxmint.com/applets/view/79"><b>Multicore System Monitor</b></a>

###  Dock 

Install <a href="https://launchpad.net/plank"><b>plank</b></a> dock from software manager

#### <a href="https://www.gnome-look.org/p/1257556/"><b>Cyberpunk plank theme</b></a>

Extract zip files to `/usr/share/plank/themes/`
	
###  Boot Logo 
	
#### <a href="https://github.com/topics/plymouth-themes"><b>Plymouth Themes</b></a>

Copy theme folder to `/usr/share/plymouth/themes/`
	
#### Install the new theme (<a href="https://raw.githubusercontent.com/adi1090x/files/master/plymouth-themes/previews/22.gif"><b>cybernetic</b></a> in this case)
```
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/cybernetic/cybernetic.plymouth 100
sudo update-alternatives --config default.plymouth
sudo update-initramfs -u	
```
	
***
**[⬆ BACK TO TOP ⬆](#contents)**

<h2 align="center">📥<b><i>SOFTWARES</b></i>📥</h2>

### <a href="https://www.oracle.com/java/technologies/downloads/"><b>Java</b></a> (Running Programs)

_VERSION 17_
```
wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.deb
chmod +x jdk-17_linux-x64_bin.deb
sudo dpkg -i jdk-17_linux-x64_bin.deb
```

_VERSION 21_
```
wget https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.deb
chmod +x jdk-21_linux-x64_bin.deb
sudo dpkg -i jdk-21_linux-x64_bin.deb
```	
	
###  <a href="https://www.winehq.org/"><b>Wine</b></a> (Install Windows Softwares) 
```
sudo dpkg --add-architecture i386 
wget -nc https://dl.winehq.org/wine-builds/winehq.key
sudo apt-key add winehq.key
sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main' 
sudo apt install --install-recommends winehq-stable
```

###  <a href="https://www.qbittorrent.org/"><b>qBittorrent</b></a> (Torrenting Client) 
```	
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt-get update
sudo apt install qbittorrent
```

###  <a href="https://github.com/lpereira/hardinfo"><b>Hardinfo</b></a> (System Information)  
```
sudo add-apt-repository ppa:linuxuprising/hardinfo
sudo apt update
sudo apt install hardinfo
```

###  <a href="https://www.bleachbit.org/features"><b>Bleachbit</b></a> (Clean System) 
 ```
sudo apt install bleachbit
```	

###  <a href="https://oguzhaninan.github.io/Stacer-Web/"><b>Stacer</b></a> (System Optimizer & Monitoring) 
```
sudo add-apt-repository ppa:oguzhaninan/stacer -y
sudo apt-get update
sudo apt-get install stacer -y
```

***

For the complete guide with all sections including Retro Gaming, Terminal Customization, and Linux Resources, please visit the original repository:

- https://github.com/trinib/Awesome-Mint-Setup

This README has been partially adapted from the original work by trinib.
