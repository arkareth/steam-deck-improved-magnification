# Intro
As for a visually impaired person, the default Steam Deck magnification tool's (steam button + L1) zoom factor was never enough for me to play anything requiring any amount of reading in the portable mode. I know I'm not the only one having this issue - there are posts on Steam Community forums, Reddit and Github asking @ValveSoftware to address this for years. Here's even a [feature request](https://github.com/ValveSoftware/gamescope/issues/929) in the Gamescope repo from the wonderful [Deck Text](https://github.com/mmatis/DeckText) plugin author, which had exactly zero attention from them.

Hardcoding a 1.5 zoom factor is a bad decision, and makes me think the feature was an afterthought. Not allowing users to customize it easily is even worse, and really has no reason to be this way - it's not a complicated thing for Valve devs to expose the necessary parameters.

I've mostly been sticking to Swich over the years due to this, but recently decided to deal with it finally. It's quite hacky, but once you configure it it'll just work (until some OS update breaks it, I guess).

Not into Steam Deck that much to dive into the plugin development, but I'm pretty sure there are plenty of ways to wrap this into a more user-firendly tool - if someone decides to do that - would be great.

Mandatory disclaimer: make these changes at your own risk, I'm not responsible for any issues / harm you deal to your system in the process or after. It's assumed that the user has at least minimal knowledge of bash and Linux.

With that said - send me a message if you need any help.

# How-to
1. Go to Desktop mode
2. Open terminal, navigate to your home dir: ``cd /home/deck``
3. Create a file called ``.xbindkeysrc``
4. Copy the contents of ``xbindkeysrc-sample`` from ths repo to your file
5. Now we need to ensure that in Gaming mode:
* ``xbindkeys`` is running
* STEAM_SCREEN_MAGNIFICATION property exists and set to its default value  
There are several ways to achieve that, all comes down to running a bash script in Gaming mode.  
I recommend using [Bash shortcuts](https://github.com/Tormak9970/bash-shortcuts) plugin for [Decky](https://github.com/SteamDeckHomebrew/decky-loader) - it's just more straightforward and convenient. Next steps will be described with this method in mind.  
Any other method, however - e.g., launching a terminal app from Gaming mode and running necessary commands, or adding a bash script as a non-Steam game to the library - should work as well.
6. Reboot
7. Return to Gaming mode
8. Create a new shortcut in Bash shortcuts with the following contents:
``xprop -root -f STEAM_SCREEN_MAGNIFICATION 32c -set STEAM_SCREEN_MAGNIFICATION 65535 && xbindkeys``  
Ensure that "Does this launch an app?" option is toggled
9. Launch the shortcut. It'll now be running as one of your games. Enure not to close it
10. Now press the "Steam" key, get back to your library and launch any game. Once in, pressing ``ctrl + shift + =`` will be increasing zoom, ``ctrl + shift + -`` will be decreasing it (if you're using the default xbindkeys settings from the sample file)  
There's a certain zoom level from which it'll start to get a bit laggy, but overall I haven't ecountered any crashes or lags making it impossible to navigate the screen at those zoom levels
11. For convenience - create couple of macros in the Steam controller options to bind zoom in / out combinations to the deck's back buttons. I use L4 to zoom in, L5 to zoom out.  
And also ensure the right touchpad is set to "mouse" - once zoomed in, you'll be able to navigate around the magnified screen this wasy.   

# Customization
There are two basic things you can do:

1. Change magnification step size
2. Change key combinations that trigger zoom in / out  

To change the 1st - update the MAGN=$((MAGN+50000)) to whatever increment that works best for you.  
To change the 2nd - run ``xbindkeys --multikey`` from your terminal, press the button combination and use the output to determine the proper syntax to use in ``.xbindkeysrc``. Then change ``Control+Shift + equal`` and ``Control+Shift + minus`` to whatever you need.  
Avoid using combinations like ``Shift + -`` (which maps to an underscore) and various single-character entries and anything else that can break your input. Otherwise you'll have to fiddle with settings and reboot to revert the chagnes.  
In general, not every button combination will work well, it's a trial and error effort.  