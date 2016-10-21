# HLDS-appmanifest

This repo is for reference of a legacy issue that should now be resolved. 

https://danielgibbs.co.uk/2013/11/hlds-steamcmd-workaround-appid-90/

**UPDATE: It appears that Valve may of resolved this issue as I have tested without using the files and it now works first time. I will however leave the details here for reference.**

HLDS (GoldSrc) games use appid 90 to download  the server files from SteamCMD. There is a bug that requires you to try and download the serverfiles many times before it starts downloading all the assets. I have found a fix to this problem (After much trial and error).

This fix should work with both Windows and Linux servers.

*update: I have found that the -beta beta flag is not really required. Only the correct appmanifest files are required.*

HLDS Servers

Servers this fix is useful for.

HLDS for Half-Life and Counter-Strike 1.6	90
Counter-Strike: Condition Zero dedicated server	90	+app_update 90 +app_set_config “90 mod czero”
Deathmatch Classic dedicated server	90	+app_update 90 +app_set_config “90 mod dmc”
Day of Defeat dedicated server	90	+app_update 90 +app_set_config “90 mod dod”
Half-Life: Opposing Force dedicated server	90	+app_update 90 +app_set_config “90 mod gearbox”
Ricochet dedicated server	90	+app_update 90 +app_set_config “90 mod ricochet”
Team Fortress Classic dedicated server	90	+app_update 90 +app_set_config “90 mod tfc”

How to Fix
=========

I found the workaround while working on Linux Game Server Managers.

To fix the problem you require the correct appmanifest files to be pre-installed in the game server directory as for some reason the ones SteamCMD downloads rarely work first time.

Install the Server

Try downloading the server assets from SteamCMD once as you would normally.

For example:

    ./steamcmd.sh +login anonymous +force_install_dir "/home/csserver/serverfiles" +app_update 90 +app_set_config 90 mod czero validate +quit

You will notice that the download completed quickly. This indicates that the server did not download the files correctly.

Download the appmanifest files

Once the first download attempt is completed SteamCMD will of created a directory with a long name similar to the following within the install directory:

ec5da605084840d3d7b3ed355e48c098b28a1bd5
appmanifest folder

Delete all files in this directory.

Instead download the following files to this directory.

http://danielgibbs.co.uk/appmanifest_90.acf
http://danielgibbs.co.uk/appmanifest_70.acf
http://danielgibbs.co.uk/appmanifest_10.acf
Retry using SteamCMD to download the server assets.

Half-Life, Half-Life: Deathmatch Classic and Counter Strike assets will of now downloaded.

For any servers that are a “mod”, for example +app_update 90 +app_set_config “90 mod czero” see ‘Download “mod” games’.

I recommend trying to download a couple of times just to make sure everything has worked.

Fix “mod” games

Once completing the previous step; If you are trying to install the following games an extra step is required. Replace appmanifest_90.acf with one specific to the server you want to install from the list below.

note: I am still missing some appmanifest but will add them when possible.

Counter Strike: Condition Zero
http://danielgibbs.co.uk/czero/appmanifest_90.acf
Day of Defeat
http://danielgibbs.co.uk/dod/appmanifest_90.acf
Half-Life: Opposing Force
Ricochet
Team Fortress Classic
http://danielgibbs.co.uk/tfc/appmanifest_90.acf
When replaced once again run SteamCMD and the assets for that server will now download.

Hopefully this will save you several hours trying to install a HLDS server.
