---
layout: page
title: Setup
root: .
---

You need to download some files to follow this lesson.

1. Download [data-shell.zip][zip-file] and move the file to your Desktop.
2. Unzip/extract the file.
   **Let your instructor know if you need help with this step**.
   You should end up with a new folder called **`data-shell`** on your Desktop.
3. Open a terminal.
   If you're not sure how to open a terminal in your operating system, see the instructions below.
4. In the terminal type `cd` then press the <kbd>Return</kbd> key.
   This step will make sure you start with your home folder as your working directory.

In the lesson, you will find out how to access the data files in this folder.

> ## Where to type commands: How to open a new shell
>
> The shell is a program that enables us to send commands to the computer and receive output.
> It is also referred to as the terminal or command line.
>
> Some computers include a default Unix Shell program.
> The steps below describe some methods for identifying and opening
> a Unix Shell program if you already have one installed.
> There are also options for identifying and downloading a Unix Shell program,
> a Linux/UNIX emulator, or a program to access a Unix Shell on a server.
>
> If none of the options below address your circumstances,
> try an online search for: Unix shell [your computer model] [your operating system].
{: .callout}

{::options parse_block_html="true" /}
<div>
<ul class="nav nav-tabs nav-justified" role="tablist">
<li role="presentation" class="active"><a data-os="jupyterhub" href="#jupyterhub" aria-controls="JupyterHub" role="tab" data-toggle="tab">JupyterHub</a></li>
<li role="presentation"><a data-os="windows" href="#windows" aria-controls="Windows" role="tab" data-toggle="tab">Windows</a></li>
<li role="presentation"><a data-os="macos" href="#macos" aria-controls="macOS" role="tab" data-toggle="tab">macOS</a></li>
<li role="presentation"><a data-os="linux" href="#linux" aria-controls="Linux" role="tab" data-toggle="tab">Linux</a></li>
</ul>

<div class="tab-content">
<article role="tabpanel" class="tab-pane active" id="jupyterhub">
We're currently trialing providing the course via JupyterHub.
  
You will need to connect to the Cardiff University VPN service in order to access the JupyterHub website. Please follow this link for more information:  
[https://intranet.cardiff.ac.uk/staff/supporting-your-work/it-support/wireless-and-remote-access/off-campus-access/virtual-private-network-vpn][vpn]

You can access the service at: [https://host095.sparrow.cf.ac.uk][sparrow]  
You will be presented with a warning when accessing the service as we are currently using self-signed security certificates. Please do not be alarmed and click to accept the risk in your browser.
  
Once you've logged in, please click on the "Terminal" button on the page to access a terminal environment you can use to run the commands featured in this course. The course material and the data-shell.zip file have already been added to the envrionement as wel and are available in the desktop folder.


**Accounts**
  
Please use the following accounts to access the service. We'll provide the password during the sessions.

* training1 through to training20
</article>

<article role="tabpanel" class="tab-pane" id="windows">
Computers with Windows operating systems do not automatically have a Unix Shell program
installed.
In this lesson, we encourage you to use an emulator included in Git for Windows,
which gives you access to both Bash shell commands and Git.
If you are attending a Software Carpentry workshop session,
it is likely you have already received instructions on how to install Git for Windows.

Once installed, you can open a terminal by running the program Git Bash from the Windows start
menu.

Other solutions are available for running Bash commands on Windows.
There is now a Bash shell command-line tool available for Windows 10.
Additionally, you can run Bash commands on a remote computer or server that already has
a Unix Shell, from your Windows machine.
This can usually be done through a Secure Shell (SSH) client.
One such client available for free for Windows computers is PuTTY.
See the reference below for information on installing and using PuTTY,
using the Windows 10 command-line tool, or installing and using a Unix/Linux emulator.

**Reference**

* [Git for Windows][git4windows] - *Recommended*

**For advanced users, you may choose one of the following alternatives:**

* [Install the Windows Subsystem for Linux][wsl]
* [Using a Unix/Linux emulator (Cygwin) or Secure Shell (SSH) client (Putty)][cygwin-putty]

Please note that commands in the Windows Subsystem for Linux (WSL) or Cygwin may differ slightly
from those shown in the lesson or presented in the workshop.
</article>

<article role="tabpanel" class="tab-pane" id="macos">
For a Mac computer running macOS Mojave or earlier releases, the default Unix Shell is Bash.
For a Mac computer running macOS Catalina or later releases, the default Unix Shell is Zsh.
Your default shell is available via the Terminal program within your Utilities folder.

To open Terminal, try one or both of the following:
* In Finder, select the Go menu, then select Utilities.
  Locate Terminal in the Utilities folder and open it.
* Use the Mac 'Spotlight' computer search function.
  Search for: `Terminal` and press <kbd>Return</kbd>.

To check if your machine is set up to use something other than Bash,
type `echo $SHELL` in your terminal window.

If your machine is set up to use something other than Bash,
you can run it by opening a terminal and typing `bash`.

[How to Use Terminal on a Mac][mac-terminal]
</article>

<article role="tabpanel" class="tab-pane" id="linux">
The default Unix Shell for Linux operating systems is usually Bash.
On most versions of Linux, it is accessible by running the
[Gnome Terminal][gnome-terminal] or [KDE Konsole][kde-konsole] or [xterm][xterm],
which can be found via the applications menu or the search bar.
If your machine is set up to use something other than Bash,
you can run it by opening a terminal and typing `bash`.
</article>
</div>
</div>

[zip-file]: {{ page.root }}/data/data-shell.zip
[git4windows]: https://gitforwindows.org/
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
[cygwin-putty]: http://faculty.smu.edu/reynolds/unixtut/windows.html
[mac-terminal]: http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/
[gnome-terminal]: https://help.gnome.org/users/gnome-terminal/stable/
[kde-konsole]: https://konsole.kde.org/
[xterm]: https://en.wikipedia.org/wiki/Xterm
[sparrow]: https://host095.sparrow.cf.ac.uk
[vpn]: https://intranet.cardiff.ac.uk/staff/supporting-your-work/it-support/wireless-and-remote-access/off-campus-access/virtual-private-network-vpn
