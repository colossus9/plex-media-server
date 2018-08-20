# plex-media-server

I needed a way to make my many DVDs and Blu-rays available easily, but didn't want to store all of them on a bookshelf for aesthetic reasons. Therefore, we chose to store them on our Plex Media Server.

Below are some notes on how it was setup.

## Server Specifications

- **Model:** HP Pavilion dv7
- **OS:** Ubuntu 18.04.1 LTS (64-bit)
- **CPU:** Intel Core i7-2630QM
- **Memory:** 12 GB
- **Disk:** 4 TB

## Setup
These are the steps following during the initial setup. The original version of Plex Media Server used was `plexmediaserver_1.13.4.5271-200287a06_amd64.deb`.

- Install `ubuntu-18.04.1-desktop-amd64` on HP Pavilion dv7
	- During install, selected the following options
		- :ballot_box_with_check: Minimal installation (Web browser and basic utilities)
		- :ballot_box_with_check: Download updates while installing Ubuntu
		- :ballot_box_with_check: Install third-party software for graphics and Wi-Fi hardware and additional media formats
	- Created username `plex`
- Verified updates were installed
- Created the following directories:
	- `/workspace` owned by `plex`
	- `/workspace/plex/media`
	- `/workspace/plex/software`
	- `/workspace/plex/backups`
- [Installed SSH Server](https://help.ubuntu.com/lts/serverguide/openssh-server.html.en)  (kept default values) and networking tools
	- `sudo apt install curl openssh-client openssh-server net-tools`
	- Setup ssh key pair
- Copied `plexmediaserver_1.13.4.5271-200287a06_amd64.deb` to `/workspace/plex/software`
- Follow [Installation Article](https://support.plex.tv/articles/200288586-installation/)
	- **Preparation**
		- Consider and follow the recommended naming format
		- Created directories:
			- `/workspace/Movies`
			- `/workspace/TV Shows`
			- `/workspace/TV Shows - Bonus Features`
			- `/workspace/Music`
			- `/workspace/Photos`
			- `/workspace/Other Videos`
	- **Server Installation**
		- `cd /workspace/software`
		- `sudo dpkg -i plexmediaserver_1.13.4.5271-200287a06_amd64.deb`
		- Access the Plex Web App at `http://IP_ADDR:32400/web`
			- Signed in using my account
		- **Disabled** the option “Allow me to access my media outside my home”
- Added Libraries and pointed to directories above (from the **Preparation** section)
	- Movies
	- TV Shows
  - TV Shows - Bonus Features
  - Music
  - Photos
  - Other Videos
- Plex Settings:
	- General
		- **Disabled** the option “Send crash reports to Plex”
	- Remote Access
		- Verified Remote Access is **Disabled**
	- Scheduled Tasks
		- Update **Backup Directory** to `/workspace/plex/backups`
- Installed Tools
	- Opened **GNOME Tweaks**
		- Go to **Power** and disable “Suspend when laptop lid is closed”
- Created `ext4` partition on external drive, ran `sudo nano -w /etc/fstab`, and added the following:
	- `/dev/sdb1 /workspace/mount/WDMyBookDuo ext4 rw 0 0`

## Upgrading
To upgrade Plex Media Server on Ubuntu:

1. Find the URL for the latest Plex Media Server package [here](https://www.plex.tv/media-server-downloads/).
	- Look for `Ubuntu 64-bit ...`
2. Copy the link into your clipboard to use in the following steps.
3. SSH into the server.
4. Run the following command to download the package (example shown below):

```
wget https://downloads.plex.tv/plex-media-server/1.13.5.5291-6fa5e50a8/plexmediaserver_1.13.5.5291-6fa5e50a8_amd64.deb
```

5. Install the package with this command (example shown below):

```
sudo dpkg -i plexmediaserver_1.13.5.5291-6fa5e50a8_amd64.deb
```

6. After installation, remove the installer file with:

```
rm plexmediaserver_1.13.5.5291-6fa5e50a8_amd64.deb
```
