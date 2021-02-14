# Build Versus Buy Does Not Scale

### At a Small Scale

You just download stuff and use it.  No problem.  Or you contract with some vendor to provide a service.  No problem.

I either case, you get to hope that the author(s) continue to maintain their code.

At some point, the size of what you're doing changes that "no problem" to "big problem."  It seems to happen without warning, but happen it does.

### At a Medium Scale

You have three options.

 + Build
 + Buy (or download or contract for a service)
 + Hybrid
 
If you build your business system then you own it.  It's yours, with all that entails.  You have the ability to make it do anything you want.  With ability comes responsibility.  No one is going to make those changes for you.

If you buy (or download or contract for as a service) your business system, then it does whatever the vendor made it do.  If you need it to do something additional, you pay for it.  If you can afford it.  And don't forget their lawyers are better than yours, and the contract probably doesn't say what you think it says.

If you build pieces of your business system and obtain other pieces from one or more third parties, then you have the best and worst of both worlds.  You are responsible for your pieces and their interfaces to those from third parties.  As the third parties make changes, you must also.  Sharing responsibility means that when something goes wrong, everyone accuses everyone else of being at fault.  Be prepared to prove it's not your problem to fix.  If the problem is with a third party, be prepared to prove it, and then be prepared to pay them to fix it.

Special case: one or more of the third parties is an open source package or library.  You may be able to (or have to) fix it yourself, if the maintainers are willing to accept your pull request.  Provided you don't discover the project has been abandoned. 

### At a Large Scale

Build is your only option.  Look at what Facebook, Amazon, Netflix, and Google do -- they build their own.  They even go so far as to build their own file system, their own version of the OS, their own clustering, their own databases, their own bloody hardware.

### So What?

Welcome to IT.  If none of this sounds like your idea of a good time, find something else to do for a living.