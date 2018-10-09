pBook
=====

Self-contained offline ebooks on your pebble


Getting started
===============

- Install Pebble SDK (tested with v4.5, should work with v3+, presumably would work with cloudpebble)
- Clone pBook from github
- pebble build
- Load to your watch and read some Washington Irving; Rip Van Winkle and The Legend of Sleepy Hollow are already baked in as a demo


Adding your own books
=====================

- Every app is limited to 256KB of resources after compression (128KB for OG pebble), so some books may need to be split into chunks, each of which will be embedded in its own app as follows:
- Clone a new copy of pBook and delete all the txt and/or txt.apraw files in resources/notes
- Edit author, displayName, and name in package.json, and change the uuid (every app must have a unique uuid)
- A "note" is limited by default to 10000 bytes, so the chunk must be further split into &lt;10kB files; try "split --verbose --line-bytes=10000 -a 1 --additional-suffix=.txt mybookorchunk.txt note"
- Each note must be compressed using the modified appack compressor in the resources folder; try "for f in note*.txt; do ./appack c "$f" "$f.apraw"; done;"
- Notes larger than 10kB load and change pages a little more slowly, but compress better. I've successfully tested sizes up to 30kB with compression (and up to 50kB before I added compression) on a Pebble 2. Change TEXT\_BUFFER\_LEN in main.c and adjust --line-bytes in the split command to match.
- You can have up to 26 note files, named by default notea.txt, noteb.txt, through at most notez.txt
- Each note file must be listed in the media array in package.json; add or remove elements as necessary, following the pattern NOTE0:notea.txt, NOTE1:noteb.txt ... NOTE25:notez.txt
- Set NUM_NOTES in "Config this to fit your needs." in main.c equal to the number of note files
- Build, and download to your pebble; repeat for each chunk of the book if necessary


Usage
=====
- Select the needed note
- Single push up/down to advance a whole screen
- Double push up/down to go to the top/bottom
- Long push up/down for fast scrolling
- Single push select to activate/deactivate continuous scrolling (todo: adjustable scrolling rate)
- At the end of each note, simply go back and select the next note to continue reading (todo: advance to next note)
- Last note read and position in each note will be saved automatically on exit


Known Issues
============
- Note menu previews are broken because I need to adapt them to compressed resources, but doesn't seem to affect functionality otherwise so not a high priority, sorry.

 
Extra
=====

You can buy a drink for debuti, the author of the original Pebble Notepad upon which this is largely based, at https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=ZWE8DKMCP6ENJ

I'll accept tips for my contribution at bitcoin address 33djsmdX8pK91zhvGeZVEKdKMB7b6Zraa4


License
=======
```
                    GNU GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007
```
