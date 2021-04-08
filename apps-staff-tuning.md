Applications staff - you gotta rise up!

SMF, Language Environment, threadsafe applications in CICS, multi-row operations in DB2, standardized exception handling, application tuning...

Someone has to understand this stuff.  If not you, then who?

"I don't know," is simply unacceptable.  Your Systems Programmers are your friends, providing stable environments in which your applications can execute, but they cannot know the details of your applications.  That's on you.

No it's not?  So when you eventually have a throughput problem and the solution is to make your CICS code threadsafe, do you know what that means?  Do you think your management or your users will be happy with bad response times and/or higher bills while you figure it out?  We all remember how well the slogan "Can't someone else do it?" [worked out](https://en.wikipedia.org/wiki/Trash_of_the_Titans).

If your employer wants any of that then they have to train you?  It's a new century, application staff don't get training (of course it's shortsighted and silly and wrong, but the new normal is a race to the bottom).  If you don't know something, dig into [Redbooks](https://www.redbooks.ibm.com), dig into the [IBM Documentation](https://www.ibm.com/docs/en) for your product, *read*.

Other than "we've always done it this way," why are you still coding single row FETCH and INSERT DB2 operations?  Just because that was the only way your ancestors could code it, that doesn't mean you have to waste limited resources paying obeisance to a time-honored but now known to be inefficient method.

Have you run your applications with RPTOPTS(ON) (use CLER in CICS)?  How about RPTSTG(ON)?  Have you looked at storage tuning?  Do you know you can just add a CEEOPTS DD to change the LE options, or that you can do the same with a PARM?  Has your CICS Systems Programmer set AUTODST=YES?  Is RUWAPOOL=YES?  What is the ARCH level in your compile options?

Do you have an application profiler?  Do you use it?

Why in the world would you _not_ go digging in SMF data for application tuning opportunities?  The Systems folks might look for system tuning opportunities, but they're most likely to regard applications as black boxes, i.e. as _your_ responsibility.

Seriously, this is all very cool stuff.  Expressing an interest shows you care about more than the next deadline.  Yes, I know you're constantly being told about the importance of that deadline, but the reality is that performance and resource utilization fall into the *well of course those are important too* category.  If you hit your deadline with an application that performs badly and/or consumes resources like [Mr. Creosote](https://en.wikipedia.org/wiki/Mr_Creosote) consumes dinner, someone's going to have to rework it; even if that someone isn't you, that just means you'll end up reworking someone else's bad decisions - don't contribute to the overall depth of the problem swamp.

It's important to do the right things, it's also important to do things right.  Just because something works doesn't mean it works well, try to make sure it does both.