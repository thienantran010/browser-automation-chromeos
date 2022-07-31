# How To Set Up Browser Automation on ChromeOS

## Preface
This document was never supposed to exist. I had originally wanted to try web scraping using Selenium on my Chromebook (I activated the Linux development environment), but to my surprise, setting up Selenium, Chrome, and Firefox took 3 days. This is partly due to my inexperience, but also because there isn't a good, up-to-date guide on how to get Selenium working with Chrome and Firefox on ChromeOS. While people on Windows, Linus, and MacOS were able to stand on the shoulder of giants (they have hella resources), I had to stand on the ground.

Matt Gosden articulated this issue perfectly in his [article](https://medium.com/swlh/is-a-chromebook-good-for-coding-and-data-science-322babcd5512):

>Installing what you need to use Python or a similar language is a bit of a daunting task for a beginner on any system. In Chrome OS is particularly tricky >for beginners because it’s not so well documented or supported.
>
>There is a chicken-and-egg problem here in that there are few developers using Chromebooks for development today and therefore there are fewer tools and >how-to guides to help new coders with the issues and installs.

This chicken-and-egg problem can have serious consequences, one of which is that it can make learning to code discouraging for people without much money (this is just my reasoning I have no statistics to back me up lol). If you don't have a lot of money like me, Chromebooks are super attractive because they're cheaper than other laptops but they're still robust. So you get a Chromebook, happy with your purchase, only to hit a wall with installations that should be simple. You're not even coding yet but you're still having so much trouble. It feels awful, and exhausting if you spent hours finding a solution like me. It might even turn you away from coding.

I hope that this document can spare someone the hours I spent on getting Selenium to work with Chrome and Firefox. And if you're feeling bitter, take comfort in the fact that it only gets better from here. Coding is super fun. And maybe one day, you can help contribute your own discoveries. Be the giant you want to see in the world :)

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
