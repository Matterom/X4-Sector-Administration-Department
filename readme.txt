/* This is the forum post. */
This is a small taste of a fairly large work in progress mod. Many features are not implemented or even coded. This is the framework step for a lot of work and should be treated as such
Simply put this is a featureset for Sector Administration, Taxation and Automation. Set it up and forget it.
This release is intended to Test and Acquire feedback on the rates and balancing of the taxation feature ONLY.

[b][u][color=#FF0000]DISCLAIMER: THIS IS HEAVY WORK IN PROGRESS AND SHOULD NOT BE USED ON A PRIMARY SAVE[/color][/u][/b]

Features Implemented:
[list]
[*] Station's with managers will be forced to pay a tax periodically
[*] Trade Ships pay a tax on profits made every time they sell wares to a station
[*] This Tax Varies based on faction
[/list]

TODO Features:
[list]
[*] Immediate plans for a 1.0:
[list]
[*] Resistance values, Overtaxing Penalties and Not Paying Tax Penalties.
[*] Balancing based on feedback
[*] Sector Administrators 
[*] Tax Breaks based on factors including but not limited to, Newly constructed Station, Ships Patrolling Sector, Killing Hostiles of the parent faction.
[/list]
[*]Future
[list]
[*] Flesh Out Sales Tax (Note, May ruin current compatibility with trade mods. will see what i can do.)
[*] Replace Destroyed Ships assigned to station
[*] Sector Mine layers
[*] Support for Faction Funds
[*] Perks/Flags
[*] "Civilian Faction" that builds stations to be taxed. [ Optional Addon ]
[/list]
[/list]

Known Bugs:
[list]
[*] A Hang Can occur at the loading of a older game for seemingly no reason, This can be fixed by closing out the game, killing the process in the task manager and steam and trying again. No Error will display in the log, and i'm still trying to track it down
[*]The game can crash upon exiting the game with the mod installed... this one is new.
[*]There is many placeholder text for future features.
[*]Not all stations are recognized for taxes
[*]Unmanned stations are not taxed.
[/list]

[u]Compatibility Notes:[/u]
This system is intended to be flexible enough to be put into any redesign, rework, re-balance, whatever you want to call it. I heavily change only 1 vanilla file (trade.station) and tack on a bit to manager conversations.
If someone was wishing to rebalance this mod, all they would need to do is perform the following check a little after loading the game and it will overwrite my default setup.
[code]
<do_if value="global.taxesInitialized">
	<set_value name="global.$taxtable" exact="table[
		{faction.player} = table[{'$flags'} = [], {'$prop'} = 0.005, {'$sales'} = 0.003, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.alliance} = table[{'$flags'} = [], {'$prop'} = 0.005, {'$sales'} = 0.003, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.antigone} = table[{'$flags'} = [], {'$prop'} = 0.004, {'$sales'} = 0.006, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.argon} = table[{'$flags'} = [], {'$prop'} = 0.007, {'$sales'} = 0.006, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.civilian} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.criminal} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.hatikvah} = table[{'$flags'} = [], {'$prop'} = 0.001, {'$sales'} = 0.001, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.holyorder} = table[{'$flags'} = [], {'$prop'} = 0.001, {'$sales'} = 0.001, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.khaak} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.ministry} = table[{'$flags'} = [], {'$prop'} = 0.003, {'$sales'} = 0.002, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.ownerless} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.paranid} = table[{'$flags'} = [], {'$prop'} = 0.001, {'$sales'} = 0.01, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.scaleplate} = table[{'$flags'} = [], {'$prop'} = 0.001, {'$sales'} = 0.001, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.smuggler} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.teladi} = table[{'$flags'} = [], {'$prop'} = 0.003, {'$sales'} = 0.003, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.visitor} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]],
		{faction.xenon} = table[{'$flags'} = [], {'$prop'} = 0.000, {'$sales'} = 0.000, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]]
	]"/>	
</do_if>
[/code]

For mods that add new factions, you can simply add to this by performing the following at any time once. Or don't They'll inherit a basic 0.5% tax rate.
[code]
<set_value name="global.$taxtable.[faction.YOURFACTION]" exact="table[{'$flags'} = [], {'$prop'} = 0.005, {'$sales'} = 0.005, {'$resist'} = 1, {'$tariffs'} = table[], {'$wares'} = table[]] />
[/code]

And now some explanation as to what each variable does, or should do, as not all of this is in/finished.

[color=#BF8080]$flags:[/color] Flags are intended to be a special modifier on certain NPC/AI Features. Some working concepts include 'Tithes' which increase local hostility against the station that was unable to pay it's tax. 'shrewd' which pays 10% less in sales taxes. 'Democratic' where the exponential curve for being overtaxed is doubled.  [u]Unimplemented[/u]

[color=#BF8080]$prop[/color]: ex 0.005 or 0.5% of a station's value per Hour. This cash is transferred to the local owning faction's Sector Administrator.

[color=#BF8080]$sales:[/color] ex 0.005 or 0.5% of a transaction's profits. Why profits? Because it represented the best possible temporary solution to test the feature. In the future when i can apply this to the search for trade logic i may change this to total... and actually sales price. As for now it's simply a test.

[color=#BF8080]$resist:[/color] ex  ( a value between 0 and 1) The Resist Value denotes the Highest allowed rate of tax that a given faction will allow. Higher Over this is an exponential increase in "Hostility". This is mitigated by doing your job as a land lord and supplying enough ships or defenses to defending the sector against hostiles, Xenon ect. [u]Unimplemented currently[/u]

[color=#BF8080]$tariffs:[/color] ex {faction.argon} =( a value between 0 and 2) .  This represents the relational aspect between 2 factions. A faction with a tariff rating of 2 will charge 200% the normal tax rate to ships trading at their stations Whereas a value of 0.5 will denote half the base rate.[u] Unimplemented[/u]

[color=#BF8080]$wares:[/color] Basically, Tarrifs but on wares.. Very [u]Unimplemented[/u] until i can find a decent solution to set it up for the player


Change Log:
[spoiler]
v0.01 Initial testing Release
[/spoiler]




[b][u][color=#FF0000]DISCLAIMER: THIS IS HEAVY WORK IN PROGRESS AND SHOULD NOT BE USED ON A PRIMARY SAVE[/color][/u][/b]
Downloads: