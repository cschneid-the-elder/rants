I hate computers.  I mean, I _really hate_ computers.

When Microsoft decided that [CUA](https://en.wikipedia.org/wiki/IBM_Common_User_Access) wasn't spiffy enough for them and created drop down list boxes that behaved _ever-so-artistically_ differently in Encarta, we were all doomed to having to figure out how each application and each OS wanted us to tell it what to do.  Again.  And again when we upgraded.

Apple didn't help when they ditched skeuomorphism in iOS 7 and went for the accursed "flat" look popularized by Microsoft in their Metro specs.  Thanks, now I have to dig through my settings to find how to make buttons look like buttons again and to make the fonts readable.

The idea of "skins" for UIs have been around for a couple of decades, why is this not integral to OSs?  Give us the ability to change the appearance of our UIs in a variety of delightful ways instead of forcing us to accept what deluded designers deign to dump on our devices.

In the mid-1990s we learned that, to most people, the UI _is_ the system, the application, the OS.  _Don't fsck with it._  Don't make us learn how to use our apps all over again.  It's disruptive and upsetting and it _makes us angry._  Don't make us angry, we don't like being angry.

And we _get_ angry when we have to help our relatives over the phone because Facebook or Google or Apple decided to change their UI without regard for the angst it causes their users.

In a cowardly move, Apple hid the fact that they're dropping support for the iPhone 5s, 6, and 6 plus in iOS 13, forcing an unknown number of people to upgrade their hardware.  Upgrades of iDevices are fraught with uncertainty and danger, more so since Apple quit backing up the apps when the device was backed up.  Now we have to re-download all our apps and that's not fun for the millions of people without broadband access.

Apple also declines to support macOS on older hardware.  I can understand the possibility that users of underpowered machines might be unhappy with the experience, but why not let them decide for themselves?  And why not give them the option to back out the upgrade?  And what is it, _exactly_ that macOS 10.14 needs that an i7 processor with 16G of RAM cannot deliver?  Maybe users of older hardware won't make use of those features, or maybe Apple can look into degrading gracefully.  I guess not, though.

Our hardware is _fine_, it _works_ fine, we don't _want_ to upgrade to the extra-large iPhone [Mxyzptlk](https://en.wikipedia.org/wiki/Mister_Mxyzptlk) with tint control and incompatible connectors or the MacBook with a single incompatible port both for charging and connecting external devices which _of course we need_ you ninnies.  We _like_ the MagSafe connector and all the ports because not everything lives in the cloud and we need physical media and _there are millions of us without broadband access._  Ninnies.

When iOS 11 came out I looked at the feature list and found exactly zero new features that I cared about.  But I can't get the security updates without a whole new version of iOS, so I have to upgrade.  That's one iOS upgrade that I clearly remember, but most of them are like that.  It's all about Siri, which I turn off because I don't want my devices listening to me.  It's all about 3d touch, which was stupid and is being discontinued.  It's about the camera(s) which were good enough a few years ago and are not a selling point for me.

At least [IBM says](https://www.ibm.com/it-infrastructure/z/capabilities/system-integrity) they'll fix system integrity problems, neither [Apple](https://www.apple.com/legal/sla/docs/macOS1014.pdf) nor [Microsoft](https://www.microsoft.com/en-us/Useterms/Retail/Windows/10/UseTerms_Retail_Windows_10_English.htm) warrant their respective OSs for fitness for purpose _at all._  I guess I need a phone that runs z/OS.

And I simply cannot _wait_ for all the vulnerabilities iPadOS will create as it moves the iPad closer to laptop functionality.

Linux is the usual answer people provide to all these problems, but _they lie to you._  My Ubuntu box rarely goes a week without having to install some patches, and this worries me.  While Linux enthusiasts tell me this is a good thing, that bugs are being fixed, I have this uncomfortable feeling regarding the fact that the bugs were there in the first place and _I don't like that._

Yes, yes, I know, all software more complicated than "Hello, World!" has bugs, but _why?_  Rather than living with the status quo, why don't we change it?  Rather than mitigations like address space layout randomization, how about we quit implementing Turing-complete interfaces everywhere?

The problem with _being able_ to tweak a system (e.g. Linux) is that the _ability_ to do those tweaks instantly becomes the _requirement_ that you do them.  This is where I view Apple systems as superior -- if macOS can't figure it out on its own then I'm done.  No amount of tweaking will make whatever-it-is work.  With Linux or Windows, some hours of my time and my sweat and my patience must be sacrificed in order to make whatever-it-is work.  _Ability_ becomes _responsibility_ and I'm just not that young any more.  YMMV.

And I've never used a Microsoft Surface device, but I'm sure they're crap.

[The IT Crowd](https://en.wikipedia.org/wiki/The_IT_Crowd) is one of my favorites, but "Have you tried turning it off and back on again?" is supposed to be a joke, not an actual problem solution.  Yes, it made the problem go away, but the first thing that happens after that should be figuring out how to make it never happen again.

Now someone is smirking and tweeting about how I don't know that hardware has bugs too; I do know, but apparently _you're comfortable with that._  Numpty.

This is the stuff that controls your bank balance, the vehicles you ride in, the medical equipment keeping you from dying, and you're _okay_ with retry, restart, reboot, reinstall?

And security sucks.  No one seems to be able to implement it correctly, and the closer they get the more you try to circumvent it because safety is inconvenient.  Admit it, you're running with Admin privileges and you stay signed in to web sites, but you think you're safe because your bank account password is your mother's land line number.

If you're a US citizen you've probably been doxxed, you know.  With the Equifax breach in 2017, most US adults had their PII stolen.  You should probably freeze your credit before you don't have any.

It's not as if this is easy for any of us.  Every time I try to use something it wants to be patched or it turns out I wish it could be patched because it's got a vulnerability and the vendor says the solution is to buy a new device.

We're supposed to use password managers, but they're a succulent target and do occasionally get breached (OneLogin in 2017 and LastPass in 2015).  Is it better than not using one?  Better than a printed list kept in a secure place?  Better than an encrypted drive?  Does anyone know?

All of this security kerfuffle is caused by the counterintuitive problem of authentication - how can you prove that you're you.  To a computer.  Not just any computer, but a computer that's constantly barraged with attempts from people who _aren't_ you to prove that they _are_ you in order to steal your money, your identity, your life.  So you _want_ that computer to be a bit paranoid.  But also to recognize that you're you when you've forgotten your password or your PIN and it's 3 a.m. on a bank holiday and you're on vacation in foreign parts and just had your passport and wallet stolen.

Fred Brooks [pointed out](https://www.goodreads.com/author/quotes/3174788.Frederick_P_Brooks_Jr_) that we should plan to build one to throw away since we're going to anyway.  We never imagined that applied to the whole of software infrastructure created over the last half century.

__I think we need to start over.__  When computer systems are built, it's normal to gather requirements before starting to write code or even choosing an operating system and programming language and the hardware on which to run it all.  But we're coming at this from the wrong end, where we've got existing systems we want to be secure and reliable and robust so we're trying to retrofit foundational requirements into a teetering Jenga tower built by people doing the best they could with what they had at the time over the last half century.

__I think we need to start over.__  Intel and AMD (et. al. ?) have speculative execution security problems due to tricksy mechanisms they used because Moore's Law no longer holds.

__I think we need to start over.__  The [Intel Management Engine](https://en.wikipedia.org/wiki/Intel_Management_Engine) and the [AMD Platform Security Processor](https://en.wikipedia.org/wiki/AMD_Platform_Security_Processor) force you to be insecure and are [security disasters](https://www.eff.org/deeplinks/2017/05/intels-management-engine-security-hazard-and-users-need-way-disable-it) in the making.

___I think we need to start over.___

Security.  Privacy.  Loose coupling.  Fitness for purpose.  Modularity.  Efficiency.  Reliability.  Availability.  Serviceability.  Open source.  What, not how.

You see how to do it wrong.  Now do it right.

