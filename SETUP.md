# Setup Instructions

Notes about setting up this project in JetBrains Rider IDE running in Fedora 42 Desktop    
By [Chris Freeman](https://github.com/skyblue38) 2025-May-23


## Build a VM host
Create a VM and install Fedora 42 Desktop (eg in TrueNAS or ProxMox)    
see: [TrueNAS VMs](https://www.truenas.com/docs/scale/24.10/scaleuireference/virtualizationscreens/)     
[ProxMOX VMs](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/)

Make sure that all packages are up-to-date. `sudo dnf -y update`

## Docker
* Now install Docker CE in the root context (see: https://idroot.us/install-docker-desktop-fedora-42/)        
`whereis docker` should return nothing as docker should not be already installed. if it is, remove it using:        
`sudo dnf remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-selinux docker-engine-selinux docker-engine`    
* Add support for `config-manager` using: `sudo dnf install -y dnf-plugins-core`        
* Install the Docker Repository: `sudo dnf config-manager addrepo --from-repofile=https://download.docker.com/linux/fedora/docker-ce.repo`        
* Install Docker Engine: `sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`        
* Enable and Start the Docker service: `sudo systemctl enable --now docker`    
* Verify that Docker started OK: `sudo systemctl status docker`    
* Add development username to the Docker group: `sudo usermod -aG docker <username>`    
* Login as the development user and verify acess to Docker: `docker --version`    

## Install JetBrains Rider IDE
Add additional packages to support .NET and mono, if required:    
* sudo dnf install mono-complete    
* sudo dnf install dotnet-sdk-9.0    
* sudo dnf install aspnetcore-runtime-9.0    
* sudo dnf install dotnet-runtime-9.0

The easiest way to install JetBrain tools is via the JetBrains Toolbox.    
Download, unpack and run the installer from:   
`https://www.jetbrains.com/toolbox-app/download/download-thanks.html?platform=linux`    
A Jetbrains account with a paid subscription to "All-Packages" will be required...    
Once the toolbox is installed and running, you can select installation of Rider IDE.    
The following shows the status of a complete installation of Rider IDE.    
```
JetBrains Rider 2025.1.2
Build #RD-251.25410.119, built on May 7, 2025
Source revision: d31f38dce07eb
Licensed to Chris Freeman
Subscription is active until June 13, 2025.
Runtime version: 21.0.6+9-b895.109 amd64 (JCEF 122.1.9)
VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
Toolkit: sun.awt.X11.XToolkit
Linux 6.14.6-300.fc42.x86_64
Fedora Linux 42 (Workstation Edition); glibc: 2.41
.NET Core v8.0.11 x64 (Server GC)
GC: G1 Young Generation, G1 Concurrent GC, G1 Old Generation
Memory: 990M
Cores: 4
Registry:
  ide.experimental.ui=true
  llm.show.ai.promotion.window.on.start=false
Current Desktop: GNOME
```

## IDE Project
Next, create a new project in Rider by cloning from the author's github page for skad-dotnet.      
Open https://github.com/robpacheco/skad-dotnet and create a new Fork.    
in the fork, click `<>CODE` then copy the URL
https://github.com/robpacheco/skad-dotnet.git    
In JetBrains Rider IDE Projects page, select "clone a project" and  enter the URL that was copied above.    
This will populate a new project page with the cloned contents.    
... watch for any initiation issues...    
If required, apply the update/install for dotnet-ef

## Setup complete
To Be Continued if more is required...