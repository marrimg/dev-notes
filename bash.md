http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html

WHEN working with Linux, Unix, and Mac OS X, I always forget which bash config file to edit when I want to set my PATH and other environmental variables for my shell. Should you edit .bash_profile or .bashrc in your home directory?

You can put configurations in either file, and you can create either if it doesn’t exist. But why two different files? What is the difference?

According to the bash man page, .bash_profile is executed for login shells, while .bashrc is executed for interactive non-login shells.

https://scriptingosx.com/2017/04/about-bash_profile-and-bashrc-on-macos/

For example, macOS sets the PATH environment variable to /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin by default. This is a list of directories (separated by a colon ‘:’) that the system searches through in order for commands. I like to add a folder in my home directory ~/bin to that list, so that I can execute certain tools without needing to type out the full path. (e.g. munkipkg, quickpkg and ssh-installer).

There are (mainly) two user level files which bash may run when a bash shell starts. ~/.bash_profile or ~/.bashrc.

The usual convention is that .bash_profile will be executed at login shells, i.e. interactive shells where you login with your user name and password at the beginning. When you ssh into a remote host, it will ask you for user name and password (or some other authentication) to log in, so it is a login shell.

When you open a terminal application, it does not ask for login. You will just get a command prompt. In other versions of Unix or Linux, this will not run the .bash_profile but a different file .bashrc. The underlying idea is that the .bash_profile should be run only once when you login, and the .bashrc for every new interactive shell.

However, Terminal.app on macOS, does not follow this convention. When Terminal.app opens a new window, it will run .bash_profile. Not, as users familiar with other Unix systems would expect, .bashrc.

Note: The Xterm application installed as part of Xquartz runs .bashrc when a new window opens, not .bash_profile. Other third-party terminal applications on macOS may follow the precedent set by Terminal.app or not.

https://apple.stackexchange.com/questions/119711/why-doesnt-mac-os-x-source-bashrc

# PATH

https://coolestguidesontheplanet.com/add-shell-path-osx/

The shell path for a user in macOS or OSX is a set of locations in the filing system whereby the user has permissions to use certain applications, commands and programs without the need to specify the full path to that command or program in the Terminal. This will work in macOS Mojave, Sierra and all older OSX operating systems; El Capitan, Yosemite, Mavericks and Lion.
