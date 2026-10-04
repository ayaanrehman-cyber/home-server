# Home Server

A self-hosted server I built on an old laptop, running Proxmox, to learn virtualisation and Linux administration, and to give my family a private alternative to cloud photo storage.

## Why I built it

All our family photos and videos were on ONE USB stick. Even videos that used an old VHS player and had been converted to an .mp3 format; they were all on the same USB. In any case, having all the memories of childhood nostalgia on one volatile drive that could fail at any moment was a huge risk. Secondly, the family liked looking at the old photos at any point in time, so by self-hosting the photos and videos, it created an on-demand service that allowed every family member to access, upload and download these memories whenever they desired.

## Hardware

| Part | Details |
|---|---|
| Machine | HP Pavilion 15 2015 |
| CPU / RAM | Intel Core i5-4288U 2.6GHz, 8GB DDR3 |
| Storage | originally 1.5TB HDD, replaced with 250GB SATA SSD (more info in "Problems I hit and how I fixed them") |

<img width="200" height="350" alt="IMG_4379" src="https://github.com/user-attachments/assets/a0da1b1e-f091-4dc8-beef-e0b4203103e1" />



## What's running

| Service | What it does | Runs as |
|---|---|---|
| Proxmox VE | Hypervisor that hosts everything else | Bare metal |
| Immich | Self-hosted photo & video backup used by my family | LXC container |

<img width="3024" height="1781" alt="IMG_4513" src="https://github.com/user-attachments/assets/fcd1eeb8-9388-4656-97d9-f7dcb28b4133" />

<img width="1920" height="1080" alt="immich desktop" src="https://github.com/user-attachments/assets/0020c47a-4f10-433b-b377-a1916606b240" />


## How I set it up

1. Installed Proxmox onto the laptop using a bootable drive
2. Mounted and copied photos from the USB stick to the laptop's internal HDD, with no GUI, just running commands through Proxmox
3. Created the container for Immich using Proxmox Community Scripts - really helpful!
4. Set up Immich and set the location of the photos and videos to the segregated section of the internal drive where the photos and videos live.
5. Created an account in which all the photos and videos have been uploaded to, all the family members can access it either from their mobiles (see below) or from their desktops (see above)

<img width="550" height="1175" alt="immich phone" src="https://github.com/user-attachments/assets/3b39c32d-109f-4fdb-be7a-686ed4e128e1" />


## Problems I hit and how I fixed them

- One problem was that the drive (1.5TB HDD) was multitudes slower than a SSD. As a result, the local machine learning models for facial recognition would be extremely slow, whilst consuming a very large amount of RAM out of a very small supply (8GB)
- I fixed this by opening the laptop up, and replacing the internal HDD with a SSD. The CD-ROM drive was also taken out, meaning another HDD would be able to fit inside, given a HDD caddy.
- I was already aware that SSDs are a lot faster in terms of read and write speeds compared to a HDD, but i learnt HOW fast. The difference was night and day. The SSD had more than ample storage space for all the photos and videos, plus even more space for more photos and videos that are to be added perhaps in the future.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- Another problem I had was whilst trying to launch the Proxmox installer via the bootable USB stick. I was running Ventoy.exe with a custom menu, which allowed for multiple ISO files to be on the same USB stick. Proxmox was not launching at all.
- I tried booting in normal mode, then GRUB2 mode, still nothing. In the end i fixed it by wiping that USB and using Rufus.exe to burn that one ISO to the bootable USB, which worked perfectly.
- It taught me that sometimes a software can be almost perfect, but there'll always be flaws.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- Furthermore, when trying to upload the photos and videos onto the Immich server from my internal storage, it would not upload at all.
- The fix was to exclude a certain folder - I believe it was a 'lost and found directory'. Once that was excluded from uploads, everything ran smoothly.
- I had to go through almost every folder to try and pinpoint the bad apple; I was taught a strong sense of patience is required, even when it doesn't seem like there's anything at the forefront, the issue can always be resolved in time.

## Security decisions

- At the moment, its only reachable on my local home network, through the laptop's IP and the specific port number that Immich uses. I
- Set up Snapshots to be taken every couple of days, during off-hours e.g, early hours of the morning, as to not disturb processes fetching and running in the day. It also allows me to have a peace of mind to be able to tinker and put the system back exactly the way it was if anything goes wrong.

## Next steps

- [ ] Tailscale, to be able to access my home server from anywhere 
- [ ] Pi-hole - network wide ad-blocking
- [ ] Home Assistant with a local voice assistant for the lights
- [ ] Jellyfin media server

---
