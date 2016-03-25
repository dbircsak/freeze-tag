Freeze Tag 1.51b
for Quake3 1.30
by Darrell "Doolittle" Bircsak

Copy these files to C:\Program Files\Quake III Arena\freeze.  Your directory may be different.

Freeze Tag is a teamplay modification for Quake3 and Team Arena.  It is a lot like that game you may have played as a kid, but without the killing.  In Freeze Tag you try to eliminate the entire enemy team.  If you kill someone then they will become frozen.  So to eliminate all, you'd need to freeze everyone, making them all frozen at the same time.  This will give your team a point and the round will start over again.  If you are ever frozen, a teammate can come rescue you by standing next to your icy body for three seconds.  You'll then be set free and can join the battle again.

	Kill the enemy to freeze them
	Stand by a teammate for three seconds to unthaw them
	Freeze the entire enemy team to win
	Shoot an enemy opponent to "get their attention" and taunt
	Watch your back, patrol as a group
	Set traps, guard frozen enemy bodies
	While you camp your team may be getting slaughtered so make sure to save them
	You are a good player if you thaw more than one teammate at a time
	You are a great player if you are the last person alive and you perform a miraculous comeback, take out the other team and revive your teammates
	You are strategic if you only concentrate on thawing teammates; this kind of activity usually keeps a team alive
	You understand all things if you can balance this with killing the other team
	You are sneaky if you wait for enemies to come thaw their guys and then attack from the shadows
	You are fun to play with if you don't shoot the author
	For more info see http://www.planetquake.com/freeze

CLIENT

The only major new commands that have been added to Freeze Tag are "drop", "ready", and using the grapple with "+button5".  The server you are connected to must have doReady and g_grapple on for you to use them though.  If doReady is on then when a map starts, all players will need to type in "ready" at the console to begin the round.  If the grapple is turned on, you should bind a key to +button5 to be able to fire the grapple and sail around the rooms.  Do this by lowering the in-game console (press ~) and type "bind mouse2 +button5", but use whatever key you wish to assign this command to.  And with the "drop" command you can drop just about anything you're carrying:  weapons, ammo, holdable items.  This is so you can help teammates if you want.  (See next paragraph for example on how to automate this.)  Another good thing to do if you like helping unfreeze people is to turn on the team overlay so that you can know at all times where your teammates are.  This is done under the Game Options menu.  By helping a teammate unfreeze you will get a point.  These points are added to your normal score as well as shown individually to the far left on the scoreboard.  If you see an "L" near the help score, that means that person is the team leader.

An example freeze.cfg file is included.  To load this type "exec freeze.cfg" within the game console.  It is actually a complex script that allows you to drop items to share with teammates.  Once you hit the backspace key, you can press a number to drop that weapon and its ammo.  Hit backspace again to go back into normal weapon selection mode.

There is also a chase camera script in freeze.cfg.  Press 5 on the keypad to turn on the third person view.  Hit the keypad's up or down arrows to zoom in or out, and left or right to orbit the player.  The camera will remember your settings if you turn it off, by hitting 5 on the keypad again.

In Freeze you can also send voice messages to other players.  The voice commands are:

	yes
	no
	praise
	onfollow
	help
	helping

To use these, type in the console "vsay_team yes" for example.  This will play the voice "Affirmative" and also send out a text "Affirmative".  "vsay yes" would send to everyone in the game, not just teammates.  Another good one is "vtell_target onfollow", which would send "I'm following" to whomever your crosshairs are on.

cg_teamChatsOnly
cg_noVoiceChats
cg_noVoiceText
Use these settings to turn voices off accordingly.

SERVER

To run a server, it is recommended you use this command line:
	quake3 +set fs_game freeze +exec ft.config +set dedicated 2
For Team Arena it would be:
	quake3 +set fs_game freeze/missionpack +set fs_basegame missionpack +exec ft.config +set dedicated 2

This should load the ft.config settings for the game.  This text file is very important.  It tells Quake3 what we want all of our gameplay values to be.  Different values can radically effect how the modification plays.  Let's look at the example ft.config that should be included.

seta sv_hostname "Freeze Tag"
First it should be mentioned that setting dedicated to 2 means you want the entire world to know about your server.  This makes your server send its address information to a master server.  This master server is where players connect to see what server they'd like to join.  They should see Freeze Tag as your hostname.

seta g_motd "Happy Freezing!"
This is a message players see as the level is loading up.  It can say anything but keep it short.

seta sv_pure "0"
This setting is very important.  If you turn it on then it means that anyone wishing to play on your server will need to have the Freeze Tag .pk3 files or they will need to download them before joining.  This also means that any .pk3 files your server loads will be the only .pk3 files their computer loads.  This is actually a good thing.  It helps ensure that no cheating is going on.
With sv_pure set to "0", then anyone can join, even people that have never heard of Freeze Tag before.  Freeze Tag has been designed to be playable for these people.  They will not see the fancy white ice shells, but instead will see the Battle Suit effect.

seta g_gametype "3"
Currently sets the game to team deathmatch.  Setting to "4" would set it to CTF, etc.  Freeze Tag will only work with team deathmatch and CTF!

seta sv_maxclients "10"
Determines how many people total you want to allow to connect.  This setting is the single most important value as far as deciding server load.  Setting it high may result in decreased performance.

seta sv_privatePassword ""
seta sv_privateClients "0"
From the 10 player slots mentioned above, you can attach a password to any number of them.  Some servers use this if they have a busy server and would like to be able to join at any time.  If a server had nine players on it and privateClients was set to 1, then anyone wanting to join would need to type in the password to get that last player spot.  Sometimes this confuses people when they see that your server has spots open, but then try to connect and realize that those spots are reserved.

seta dmflags "0"
It's time to become confusing.  You like math, don't you?  This setting, considered to be the most important as far as gameplay is concerned, can set several different values.  The way to turn on certain values involves adding up numbers.  We do this so that we can represent several choices in one number!  It's a programming thing.  The choices are:

	No falling	8
	Fixed field of view	16
	No footsteps	32
	No item reset	64
	No team reset	128
	Weapons stay	256
	No playerclip	512
	Nightmare mode	1024

If you wanted your server to have no footsteps and no falling, you would add those numbers up.  32 and 8, which would mean dmflags should be set to "40".  Want only no playerclip and nightmare mode?  512 and 1024 is dmflags "1536".
To explain each setting: (8) no falling means you take no falling damage, (16) fixed field of view means players cannot change to that "fish-eye" display allowing them to see more to their left and right.
(32) No footsteps means what it says.
(64) No item reset, when used, means that when a team wins a round all the living players will not have their health and weapon ammo reset.  This would leave them at a disadvantage as the entire enemy team will be coming in fresh.
(128) No team reset means that when a round is won, only the losing team will be unfrozen.  The winning team still may have a few people that are frozen and that need to be saved.  This will also leave the winning team at a disadvantage conceivably.
(256) Weapons stay means what it says.
(512) No playerclip allows people to walk along those ledges and go on the roof of the original Quake3 maps without being stopped by some invisible wall.  An unfortunate side effect is that some see through floors may let you fall through them.
(1024) Nightmare mode is a special setting players had asked be put in.  It is basically hyper-Freeze Tag.  You can thaw people faster, there's a shorter max-time for being frozen, all weapons do mega-damage with lots of starting ammo.  It's Freeze on steroids.  Note that with weaponlimit (see below) set to 2048, the Gauntlet will not do super damage.

seta fraglimit "30"
seta timelimit "0"
seta capturelimit "8"
These values determine when a new map will be loaded.  A frag is a kill and a capture point is the team score.

seta rconPassword "none"
The rcon command allows people who know this password to kick players, change maps, and do various other administrative things.

seta g_friendlyFire "0"
Turn this on and you can damage teammates.  If you manage to kill them then they will just die, not freeze.

seta g_teamAutoJoin "1"
seta g_teamForceBalance "0"
When you join the game, AutoJoin will automatically assign you to a team.  ForceBalance will make it so that you cannot join a team that has more players than the other team.

seta g_warmup "20"
seta g_doWarmup "0"
When a new map starts, the game can do a warmup time, which is a countdown of twenty seconds here.  Set doWarmup to actually have it work on your server.  If you have the doReady command on (see below) then everyone will need to type in "ready" to actually start the warmup countdown.

seta g_log ""
If you want to log the game.  Note that when a person is thawed, this will be sent to the log as being the saving teammate killing the frozen player with MOD_UNKNOWN.  This was done to maintain compatibility with various log parsing programs.

seta g_password "none"
seta g_needpass "0"
You can set a password needed to play on the server.  Good for private clan matches.  Turn needpass on to activate.  This value also tells players who are looking for servers which servers are password-ed before they try to join.

seta g_banIPs ""
seta g_filterBan "1"
Servers can ban certain IPs from playing on their server.  You can use wildcards (*).  filterBan turns this setting on or off.

seta g_speed "320"
seta g_gravity "800"
seta g_knockback "1000"
These settings effect the physics of the game.  These are their default values.

seta g_quadfactor "3"
The amount of damage a player does when they have the quad powerup.

seta g_weaponrespawn "5"
seta g_weaponTeamRespawn "5"
The amount of time it takes before a weapon returns after being picked up.  This is not used if weaponstay for dmflags (mentioned above) is on.

seta g_forcerespawn "20"
seta g_inactivity "60"
The number is in seconds.  You can make someone automatically respawn if they haven't.  You can also have people kicked off of the server if they do not move for more than a minute.  These are good options.  Use them.

seta g_allowVote "1"
seta votelimit "50"
If you have allowVote on and you set up a value for votelimit, you can choose which voting options you want your players to be able to change.  The way this is set works much like dmflags where you add values together.

	map_restart	1
	nextmap	2
	map	4
	g_gametype	8
	kick	16
	clientkick	32
	g_doWarmup	64
	timelimit	128
	fraglimit	256
	g_grapple	512

The setting of "50" is nextmap, kick, and clientkick:  2, 16, and 32, which totals to 50.  (g_grapple will be mentioned below.)

seta bot_nochat "0"
seta bot_minplayers "0"
seta g_spSkill "4"
seta bot_enable "1"
You can set up bots with these values.  The bots know how to unfreeze teammates.  With minplayers, the system will make sure a certain total amount of people are playing.  If a human joins, then a bot will be removed.  When a human leaves, the bot will come back.  Set bot_enable to "0" if you do not use bots.  This will improve your server's performance as all of the bot libraries are not loaded.

seta sv_maxPing "0"
seta sv_minPing "0"
seta sv_maxRate "10000"
Perhaps you want players who have fast connections to only be allowed to play.

seta com_hunkMegs "56"
seta com_soundMegs "8"
seta com_zoneMegs "16"
These settings determine how much memory is taken away from the operating system and used for the server.  Setting hunkMegs higher than "128" is said to be pointless.  The listed settings are the default settings.

seta com_maxfps "85"
Even if someone connects with a super computer you can limit how fast their screen displays to possibly even the playing field for those with slower computers.

seta sv_floodProtect "1"
This should always be on.  Does not let people talk if they are flooding the server with comments too fast.

seta sv_master2 "master0.gamespy.com"
seta sv_master3 ""
seta sv_master4 ""
seta sv_master5 ""
These are the servers your server will contact so that their master list can let other players know your server exists.  Used with "set dedicated 2" mentioned above.

seta sv_allowDownload "1"
If you set sv_pure to "1" and leave this off, people without the Freeze .pk3 files will not be able to join, otherwise they can download within Quake3 the files they need from you.

seta wpflags "14"
This works just like dmflags and votelimit.  Pick what weapons you want people to start with on a respawn.  The weapon numbers are:

	Machinegun	1
	Shotgun	2
	Grenade Launcher	4
	Rocket Launcher	8
	Lightning Gun	16
	Railgun	32
	Plasma Gun	64
	BFG10K	128
	Nailgun	256
	Prox Launcher	512
	Chaingun	1024

If you wanted everyone to start with a Shotgun, Grenade Launcher, and Rocket Launcher, you'd add 2, 4, and 8 to get wpflags "14".  Players will always start with the Machinegun and Gauntlet as well.

seta weaponlimit "128"
Used to turn off or remove weapons and ammo types from maps.  Uses the same values as wpflags.  If you set to 1 then players will not start out with a machinegun.  Also, if nightmare dmflags mode is on and weaponlimit 2048 is used, the Gauntlet will not do super damage.

seta g_doReady "0"
If this is on then everyone must type "ready" for the level warmup to begin.  Great for clan matches.  You must have doWarmup (see above) set in order for this flag to work, naturally.  The scoreboard will show who has not typed "ready" in yet.

seta g_grapple "0"
Freeze comes with a simple grapple.  Turn it on here and then bind a key to "+button5" to use.  This grapple actually came with Quake3.  They did not have it on though to preserve map flow.

seta g_enableBreath "1"
This is also a client setting.  Turn on or off the breath puff you get from players because the arena air is so cold.  For ambiance.

seta g_startArmor "5"
Goes well with wpflags (see above).  Determines how much starting armor you respawn with.  Good for allowing the player to get a few "wake-up" hits before being frozen.

seta disable_item_quad "1"
You can turn off specific items.  Use their full name.  Some examples have been included.

An example map rotation list is included at the end.  Notice how you can switch gametypes back and forth from CTF to team deathmatch.


Female voice by Karla Palmer
Male voice and final production by Jeff "Tacos" Wros
Older sounds by Coal Shaft and Redder
Bot thaw AI by Fergus Dog
Code help from Neil "haste" Toronto

Freeze Tag is Copyright 1998, 2001, 2002 by Darrell Bircsak
http://www.planetquake.com/freeze
dbircsak@earthlink.net
