---
layout: post
title: "A quantum chemist: how I set up a new Mac for my development environment"
date: 2019-02-02
---
Testing 1, 2, 3. Ahem, hi everyone, this is my first blog. Please excuse any typos or grammar mistakes. 

This blog describes how you can set up a MacBook Pro 2017 for a development environment. As a researcher in quantum chemistry, my work involves frequently writing mathematical formulae, programming *ab initio* methods, visualizing molecules and orbitals, etc. Thus, setting up an environment with proper tools is essential to productivity. Some tools, such as Google Chrome, Dropbox, LastPass, are for general purposes, and some, such as [Avogadro](https://avogadro.cc/), [VMD](https://www.ks.uiuc.edu/Research/vmd/), [PSI4](http://www.psicode.org/developers.php), and [PySCF](https://github.com/pyscf/pyscf), are only used for my research.

Experienced Mac users or programmers may find this document trivial. But I will be happy if it can benefit a few junior fellows in my field. While **Migration Assistant** makes it easier to migrate your environments and files, I decide to set up my Mac from scratch because my previous one has too many messed-up settings. Let's get started!  

# Useful Links

There are a lot of useful resources about setting up a development environment on macOS. I personally benefitted the most from [this extensive guide](https://github.com/nicolashery/mac-dev-setup). Here are some links:

* [A beginner's guide to setting up a development environment on Mac OS X](https://github.com/nicolashery/mac-dev-setup)

* [Awesome Mac](https://github.com/jaywcjlove/awesome-mac)

# Know Your Machine

First things include choosing your language, logging in with Apple ID, and setting preferences (e.g. trackpad, Touch ID, internet accounts). Easy peasy. 

Before starting to install a bunch of packages, you can check your laptop configurations in **About This Mac -> Overview**:
    
* Processor, memory, graphics, storage
	
	* Tip: Google your MacBook release time and processor, check for technical details, such as number of cores, base frequency, GPU-support, instruction set, etc. It's good to know such information when you are 
    
* macOS version, decide whether you need an upgrade
        

# Install Applications (download-and-double-click)

Browser 

* Google Chrome

	* Sign in with gmail
    
* LastPass
	
	* Sign in with your business account, and link to your personal account
    
* Mathematica
    
* iTerm2

* Xcode and Xcode Command Line Tools (just Google it: how to install Xcode Command Line Tools)
    
* Zotero
	
	* Transfer data from the old laptop: copy the whole Zotero folder (can be found in **Zotero->Preferences->Advanced->Files** and **Folders->Data Directory Location**) to somewhere in in the new laptop, and change the data directory location of new Zotero 
    
* Slack

* Evernote
    
* Avogadro
    
* Docker
    
* Cyberduck

* CLion

* PyCharm

* Google drive

* Dropbox

* SourceTree

* MacTex (Tex Live for macOS 10.10+)

* TexStudio
    
    * Change TexStudio->System Preference->Commands using executables in /Library/Tex/texbin
    
    * Maybe, add /Library/Tex/texbin to $PATH

* VMD

* XQuartz

* MacDown

# Development Tools

Anaconda3 (currently with python 3.7)

* Find conda in `~/anaconda3/bin/conda`, add to `$PATH`
    
* Jupyter notebook is already there! Run it with command: `jupyter notebook`
    
* There is a Anaconda-bundled Python IDE called Spyder, works well for me
    
* Use conda to install psi4: `conda install psi4 psi4-rt python=3.6 -c psi4`
       
	* Note that python3.7 is downgraded to python3.6
	
* Use conda to install pyscf: `conda install -c pyscf pyscf`
       
	* Note that libxc library is missing (lib: libxc.4.dylib)
	
	* Using `conda install -c pyscf libxc`, or `port install libxc`, or `port install libxc4` didn’t provide the libxc library either
	
	* Finally, using `pip install pyscf` solved the problem, since it correctly installed libxc.4.lib library.
	
	* Note that this is Anaconda-bundled pip

Let’s try Macports this time as our package manager. The reason is that there are several chemistry/physics softwares, such as XCrysDen, that can be easily installed using port. If we don’t like Macports in the end, just uninstall it (https://guide.macports.org/chunked/installing.macports.uninstalling.html). Install some developers’ packages

* git (2.20.1): `sudo port install git`
        
	* Note that Macports is independent of your system environment. Thus, it tends to install its own dependencies.
        
	* python2.7 is a dependency of git. Now you should two python2.7’s, one is provided by macOS and one by Macports. I use the Macports one (symlinked to python2).  
       
	* Store ssh public key to github account following:
            
		* `https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/`
            
		* `https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/`
            
		* `https://help.github.com/articles/testing-your-ssh-connection/`
    
* bat: `sudo port install bat` (`https://github.com/sharkdp/bat`)
   
* ack: `sudo port install ack` (`https://beyondgrep.com/`)
   
* inkscape: `sudo port install inkscape`
        
	* Don’t forget to: `sudo port load dbus` 
        
	* Create a diretory: `$HOME/.local/share/`, otherwise inkscape will keep warning you about permissions to save files
        
	* OK, I prefer to have an inkscape app. Use command: `sudo port install inkscape-app`
    
* gimp: sudo port install gimp-app
    
Don’t use Macports to manage Python, such a pain... Use Anaconda instead. I plan to mainly use python3.
        
Notes my python commands are:
	
* `python -> ~/anaconda3/bin/python3.6`
	
* `python3 -> ~/anaconda3/bin/python3.6`
	
* `python2 -> /opt/local/bin/python2.7`

# Other developer tools:

* oh-my-zsh
        
	* Fork repository `https://github.com/robbyrussell/oh-my-zsh` so that my future changes can be stored on my github
        
	* Follow manual installation of `https://github.com/robbyrussell/oh-my-zsh`
        
	* adapt theme based on `dallas` (my new theme: `~/.oh-my-zsh/themes/dallas-adapted.zsh-theme`)
        
	* auto-completions cannot find executables in some dirs, e.g. `$HOME/bin`, `/opt/local/bin`, so I added a plugin called `zsh-completions` to `.oh-my-zsh/custom/plugins/` and edit `.zshrc`: `plugins=(… zsh-completions)`