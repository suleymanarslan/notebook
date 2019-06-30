# A Linux Distro for Developers

**P.S: [This idea became reality](http://kodfabrik.com/happy-hacking-linux)**

Brief history of my experience with Linux; My setup until 2012 was Xmonad as desktop, Emacs as editor and [Delicious Surf](http://github.com/azer/delicious-surf) as browser. Everything except the browser was command-line, I was reading news with [newsbeuter](http://newsbeuter). My distro choice was Arch. This was my zen setup; blazing fast and productive. I built a lot of stuff like [multiplayerchess.com](http://multiplayerchess.com) in quiet short time.

Then two things changed; I had to use Mac for work when I moved to US. And Arch Linux deleted its installation UI, started making changes requiring user to spend their weekend trying to fix their system after the upgrade. They could make the same changes by just having a program that upgrades the system but the culture in Arch community was like "you gotta follow the news page and follow the instructions after every change". This was a deal breaker for me because I'd like to build apps rather than spending my time configuring system. Most people in that community were system admins or people who like breaking and fixin their system. 

So I had to move on from Arch to Mac. It worked well because I worked companies using all Apple products, so just adopoted to their world. Now I left US and became an independent developer building his own stuff, I need a fast, affordable, productive system that scales to build a lot of stuff quite fast, so I can try as many ideas possible and find the idea that works well.

Recently I started installing bunch of distros in Virtualbox to see what distro meets my expectations most. I tried Ubuntu, Elementary first as they don't require users doing everything manually. But they're quite slow, and bloated by graphical interfaces as their target is end users. And I think it's a bad strategy for Linux. It needs to target developers first as open source first needs developers using it.

Then I gave Arch Linux a try, a very light-weight distro that let's you build your own desktop. It has a great concept but I think it's too low level for developers and as I mentioned before, they require users to follow news and keep updating their system manually.

As developers who are seeking a productive environment to build stuff, we are stuck between options not designed for us. When we could abstract and automate our operating systems to abstract the whole environment, we are trying to survive in one of the options. 

Recently, I'm thinking and trying to build a Linux distro based on Arch Linux. It'll target developers, installation UI will ask where your dotfiles are, do you wanna use an editor distro, which desktop environment you'd like to install. I've started the work from writing [an installation UI for Arch Linux](http://github.com/happy-hacking-linux/installer).

