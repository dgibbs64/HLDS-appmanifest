# HLDS-appmanifest
> Update October 2017:  It seems this issue has returned after Valve fixed it several years ago. I have updated this repo with new app_manifest files for each server. Hopefully Valve fix the issue again.

HLDS (GoldSrc) games use `appid 90` to download the game server files from SteamCMD.
There is a bug that prevents all the files being downloaded from SteamCMD.
Getting all the files can take any number of attempts for SteamCMD to download them all.

The fix is to download completed `appmanifest` files to the `steamapps` directory.
This fix should work with both **Windows** and **Linux** servers.

# HLDS Servers

This fix applied to the following servers:

 - Half-Life Deathmatch Dedicated Server `+app_update 90`
 - Counter-Strike 1.6  Dedicated Server `+app_update 90 +app_set_config “90 mod cstrike`
 - Counter-Strike: Condition Zero dedicated server	`+app_update 90 +app_set_config “90 mod czero”`
 - Deathmatch Classic dedicated server	`+app_update 90 +app_set_config “90 mod dmc”`
 - Day of Defeat dedicated server	`+app_update 90 +app_set_config “90 mod dod”`
 - Half-Life: Opposing Force dedicated server	`+app_update 90 +app_set_config “90 mod gearbox”`
 - Ricochet dedicated server `+app_update 90 +app_set_config “90 mod ricochet”`
 - Team Fortress Classic dedicated server `+app_update 90 +app_set_config “90 mod tfc”`

How to Fix
=========

This workaround was discovered while working on [LinuxGSM](https://gameservermanagers.com).

## Install the Server

Try downloading the server assets from SteamCMD once as you would normally.

For example:

    ./steamcmd.sh +login anonymous +force_install_dir "/home/csserver/serverfiles" +app_update 90 +app_set_config 90 mod czero validate +quit

You may notice that the download completed quickly. If this happends it indicates that the server did not download all the files correctly.

## Get appmanifest files
1. Go to the `steamapps` directory which is located with your server files and delete any existing files in the directory.
> /home/csserver/serverfiles/steamapps

2. Download the `appmanifest` files for your server from this GitHub repository in to the `steamapps` directory.

3. Retry downloading the server with SteamCMD.

It is recommended that you try and download a few times just to make sure everything has worked.