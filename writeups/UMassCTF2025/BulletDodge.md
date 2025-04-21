# Bullet Dodge
## Challenge Information
Category: Reverse Engineering

Tags: `rev` `unity` `medium` 

Points: 310

Solves: 70

Description:
This game seems unbeatable but I need to get 1000000 to win... maybe there's a secret easter egg to beat the bullets?


Given Files: [BulletDodger.zip](https://storage.googleapis.com/umassctf25-challs-static-assets-new/rev/BulletDodge/static/BulletDodger.zip)

## Approach

The challenge was a Unity-based game that required reaching a score of 1,000,000 to win.
Upon extracting the given zip i found `My project.exe`, an executable for the game and some other folders related to it, running the game I found it was practically impossible to get that high of a score through normal gameplay.

Given the fact it's a Unity game I suspected there might be a way to manipulate the game's memory since most Unity games don't have much protection against "cheating".

Note: Whilst I could've went through all the files I deemed it wasn't needed if "cheating" in the game could work.

## Exploitation

### Memory Manipulation Strategy:

I downloaded and ran CheatEngine, attaching it to the game process. It allowed me to slow down game time which revealed the score counter was independent from game time(Possibly frame based? Dosen't really matter for my solution)

### Locating the Score Value:

I set the game time to 0.01 with CheatEngine, that allowed me to just sit and wait until the score was > 10000(Wasn't 100% needed, just made the possible memory address list shorter), dying with that score, effectivly "pausing" the counter, and searching the score in memory revealed a few memory locations with the same value which I added to the Address List

### Score Modification:

Pressing "Restart" I immediately slowed down the time and tabbed into CheatEngine, selecting all the possible score addresses in the Adress List and changing their value to `1000000`, gave me the flag:

`UMASS{R4N_FR0M_B1LL_o7}`

### Thoughts

The Challenge was very fun, it reminded me of old-school singleplayer video games and how fun it was trying to cheat in them with similar tools to CheatEngine. It gave me a breath of fresh air between all the research about Japanese game developers and baud rates.
