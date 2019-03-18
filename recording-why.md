
A common trope in IT shops is the strangled cries of frustration from the staff as they attempt to determine why someone who has now left the organization wrote a particular piece of code they way they did.  Or configured a service in a particular way.  Or installed a piece of software - at all.

You see, if the *why* of it is unknown, modifications become fraught with danger.  Maybe it is the way it is for a very good reason and changing it will cause all manner of horror.  Or maybe it was the first thing someone got to work and it's just remained that way due to fear - if it ain't broke, don't fix it.  

But now it's broke, or needs an upgrade.  So we develop a workaround, in order to avoid any material change.  Because if we back away carefully, the teetering Jenga tower will continue to teeter instead of crushing our careers under a cascade of failures accompanied by multitudes cursing our name, "Why did you change it?".

We're in this situation because typically no one knows why.  Why often isn't recorded for a whole host of reasons.  

No one reads the documentation.  At least, no one who has learned that the documentation is a point-in-time snapshot of what someone thought the code did.  Then maintenance occurred and features were added and the documentation became a wall of text to scroll past on the way to the code, which is the only reflection of current functionality.  Also, the documentation probably didn't record the decisions that led to the code.

No one has time to write documentation.  Don't you understand, we've got a deadline that was set before anyone knew how long this would take, in fact it was set before we even knew what we were about to begin to think about doing and as the deadline approached we cut out everything that wasn't completely absolutely totally essential and documentation was the first thing we tossed, alternative implementations were next followed by testing of course, but documentation, that went first.  Read that last sentence out loud, very quickly, breathlessly, and see if it doesn't sound uncomfortably familiar.

No one knows where to put the documentation.  SharePoint? I know someone who insists SharePoint is a secure data store - because no one can find anything in it.  A local wiki?  Which one?  If you think you've got just one, I suggest you cast your eyes to your network and do a search.  Some LAN directory full of documents in formats no longer (completely) readable by the current version of your word processing software?  Perhaps an internal web site, under the control of that one lonely person in the corner to prevent just anyone from storing just anything?  You've probably got all of the above, the contents of which could be represented by a series of overlapping circles on a Venn diagram, different versions of almost the same content in various formats as standards changed over time.

TODO: get trading cards printed up based on the above and try to get developers to play a M:tG-esque game at conferences.

Solving this problem of recording why something was done, or done in a particular manner, is surprisingly easy: management has to make it a priority.  Okay, it's surprisingly easy for me to write, getting it done is more difficult.

Striking while the iron is hot is a good strategy.  I have found that in the wake of an emergency, following up with a calm, "And here's how we ensure that never happens again," actually works sometimes.  Sometimes it takes a few iterations of the same emergency.

What, specifically, must be done?  Again, it's easy for me to write: create the documentation in a long-lived, relatively portable format, and put it in a well-known location.  What format?  Which well-known location?  Do we need an organizational historian?  I dunno, what makes sense for your organization?  Make a recommendation to management and have them make a decision, that's what managers are paid to do.  Implementation is left as an exercise for the reader.

If you try, you might fail.  But if you don't try, you're doomed to repeat those strangled cries of frustration.  Forever.  If nothing else, document your own decisions regarding why you did things the way you did them.  Tell people where you put this amazing treasure trove.
