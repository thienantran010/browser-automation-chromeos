# How To Set Up Browser Automation on ChromeOS

## Preface
This document was never supposed to exist. I had originally wanted to try web scraping using Selenium on my Chromebook (I activated the Linux development environment), but to my surprise, setting up Selenium, Chrome, and Firefox took 3 days. This is partly due to my inexperience, but also because there isn't a good, up-to-date guide on how to get Selenium working with Chrome and Firefox on ChromeOS. There was only a lot of complicated answers to questions that were semi-related to the issues I faced.

I was honestly kinda angry. It's unfair that I had to spend so much time on setup when someone on Windows or MacOS got it done in minutes. And if they ran into trouble, they could probably find an answer within the hundreds of resources they have. 

Matt Gosden articulated this issue perfectly in his [article](https://medium.com/swlh/is-a-chromebook-good-for-coding-and-data-science-322babcd5512):

>Installing what you need to use Python or a similar language is a bit of a daunting task for a beginner on any system. In Chrome OS is particularly tricky >for beginners because it’s not so well documented or supported.
>
>There is a chicken-and-egg problem here in that there are few developers using Chromebooks for development today and therefore there are fewer tools and >how-to guides to help new coders with the issues and installs.

This chicken-and-egg problem can have serious consequences, one of which is that it puts another barrier between a person and the start of their coding journey. How can a beginner learn to code when they can't even get set up? Coding should be accessible to all, not just those who can afford laptops that run Windows, MacOS, Linux (although I'm pretty sure there are affordable options available).

I hope that this document can spare someone the hours I spent on getting Selenium to work with Chrome and Firefox. And if you're feeling bitter, take comfort in the fact that it only gets better from here. Coding is super fun. And maybe one day, you can help contribute your own discoveries. When there are no giants to stand on, dig your feet into the ground and become the giant :)

## Requirements
This document assumes that you have activated the Linux Development Environment, installed VSCode editor, and installed Python and pip (pip should come installed with Python)

## FireFox Automation
To automate FireFox, follow these steps:

1. Create your project directory and set up a virtual environment.
   - This can be done by running `python3 -m venv venv`
   - You should see a folder in your project directory called venv
   - This isn't necessary to automating FireFox but it keeps your libraries organized. You can read more about virtual environments at [RealPython](https://realpython.com/python-virtual-environments-a-primer/)
2. Download the latest release of Geckodriver installer.
   - You can do this from the command line/terminal, but I found it easier to download from [Github](https://github.com/mozilla/geckodriver/releases)
   - It'll end up in your Downloads folder, probably
3. Move geckodriver installer to your project directory and extract Geckodriver from it.
   - Extract geckodriver by running `tar xvfz geckodriver-v0.19.1-linux64.tar.gz` by replace `geckodriver-v0.19.1-linux64.tar.gz` with the name of the installer you have
4. Add Geckodriver to your PATH.
   - To do this, we will have to use a little bit of Bash. We won't need to know much, but if you're interested, here's a [Bash cheatsheet](https://devhints.io/bash)
   - PATH is a variable that holds the directories the computer will look through for executable files. Executable files include geckodriver and FireFox.
   - You can check what directories are in the PATH by running `echo $PATH`. echo prints stuff and $PATH is just calling the variable PATH. Each directory is separated by a colon (:) and will appear underlined when you hover over it (if it exists)
   - To add geckodriver to the PATH, move Geckodriver to any of the directories in the path or add the directory that Geckodriver (the project directory) is in to the PATH
     - To move geckodriver to a directory in the PATH, run `mv geckodriver /usr/local/bin` but replace `/usr/local/bin` with a directory in the PATH (`/usr/local/bin` could already be in the PATH)
     - To add the current directory to the PATH, run `export PATH="$PATH:$HOME/path/to/current/directory/from/HOME`. HOME is a variable that holds the path to the HOME directory, so in my case, it's `/home/ttran`.
5. Download Firefox for Linux.
   - You need to get the Linux version because that's the one the Linux container can access.
   - I'm not sure if you can do this in the VSCode Terminal, so I just used the terminal given when I activated Linux Development Environment.
   - Get the FireFox installer at the offical [website](https://www.mozilla.org/en-US/firefox/linux/). The installer should be in Downloads.
   - Follow the directions in this [article](https://support.mozilla.org/en-US/kb/install-firefox-linux)
   - Install libdbus-glib by running `sudo apt-get install libdbus-glib-1-2`. I have no idea what it is, it just prevents an error from coming up
6. Add /usr/local/bin to the PATH, if it isn't already in the PATH.
   - This is where the FireFox executable is located.
   - Tip: You can run `whereis FILENAME` to locate the directory of any file. In this case, `whereis firefox` should yield /usr/local/bin
7. Run `pip install selenium` to install Selenium.
8. Test if the installations worked.
   - Run the following code:
   ```
   from selenium import webdriver

   driver = webdriver.Firefox()
   ```
   -Firefox should pop up!

## Chrome Automation
To automate Chrome, follow these steps:

1. Create your project directory and set up a virtual environment.
   - This can be done by running `python3 -m venv venv`
   - You should see a folder in your project directory called venv
   - This isn't necessary to automating FireFox but it keeps your libraries organized. You can read more about virtual environments at [RealPython](https://realpython.com/python-virtual-environments-a-primer/)
2. Download chromedriver and move it to your project directory
   - Download at [Chromium website](https://chromedriver.chromium.org/downloads)
   - Should be in Downloads
3. Add chromedriver to your PATH.
   - To do this, we will have to use a little bit of Bash. We won't need to know much, but if you're interested, here's a [Bash cheatsheet](https://devhints.io/bash)
   - PATH is a variable that holds the directories the computer will look through for executable files. Executable files include chromedriver and Google Chrome.
   - You can check what directories are in the PATH by running `echo $PATH`. echo prints stuff and $PATH is just calling the variable PATH. Each directory is separated by a colon (:) and will appear underlined when you hover over it (if it exists)
   - To add chromedriver to the PATH, move chromedriver to any of the directories in the path or add the directory that chromedriver (the project directory) is in to the PATH
     - To move chromedriver to a directory in the PATH, run `mv chromedriver /usr/local/bin` but replace `/usr/local/bin` with a directory in the PATH (`/usr/local/bin` could already be in the PATH)
     - To add the current directory to the PATH, run `export PATH="$PATH:$HOME/path/to/current/directory/from/HOME`. HOME is a variable that holds the path to the HOME directory, so in my case, it's `/home/ttran`.
4. Download Google Chrome for Linux.
   - You need to get the Linux version because that's the one the Linux container can access (the Google Chrome that came with ChromeOS won't work)
   - Download at the [official website](https://www.google.com/chrome/downloads/?platform=linux)
5. Add Google Chrome to the PATH.
   - Google Chrome should be in /usr/bin, so add this to the path by running `export PATH="$PATH:/usr/bin"` if /usr/bin isn't in the PATH
   - You can check where Google Chrome is by running `whereis google-chrome`
6. Install selenium.
   - Run `pip install selenium`
8. Test if the installation worked.
   - Run the following code. Google Chrome should pop up.
   ```
   from selenium import webdriver
   driver = webdriver.Chrome()
   ```
## Persistent PATH
The directories you added to PATH will disappear whenever you exit the session/editor (basically whenever you X out of VSCode). To add the directories to PATH permanently, we will edit the the .bashrc file. You can achieve the same effect by editing the bash_profile file or profile file. You can read more [here](https://stackabuse.com/how-to-permanently-set-path-in-linux/)

1. Run `vim + ~/.bashrc`
   - This opens bashrc file in vim, a command line text editor
2. Type the letter 'o' to enter read-only mode.
3. Use the arrow keys (down arrow specifically) to move to the bottom of the file --- the last line.
4. Type the letter 'o' to enter insert mode.
5. Press shift-enter to make a new line and type `export PATH="$PATH:/paths/you/want/included"`
   - We keep the old PATH variable and add to it in case anything depends on the other paths
6. Press esc to leave insert mode.
7. Type `:wq` to save and exit.
8. You can test if the PATH persists by closing out of the editor and opening it.

## Other Things To Know
1. To move Linux files, you have to go to Files and Linux Files. You can't drag and drop into the VSCode editor.
