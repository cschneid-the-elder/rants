Age discrimination is a major contributor to why software sucks.

C'mon, you know your own head canon, software developers are young and work 100 hours a week in a converted warehouse, subsisting on junk food and caffeine, except for the ones that make a go of kale and kombucha.  But they're definitely young, and they definitely work a lot of hours.

Lots of people think that.  It's crap.  It's also at least borderline abuse of those young people.

Developers fresh out of school think they know how to build software.  They're right, with certain caveats.

 + They don't know how to build software _in your shop._
 + They don't know your organization.
 + They don't know your organization's business rules.
 + They don't know your organization's office politics.
 + They don't know your organization's users.
 + They don't know your organization's history.<sup>[1](#f01)</sup>
 
Here's something no one tells developers in school: it takes _years_ of experience to become good at software development.  This isn't one of those 10,000 hour exhortations, this is about the fact that experience is acquired over time and that experience is valuable.

It takes _years_ to learn your own common mistakes, the stuff you should go looking for when your code doesn't work.

It takes _years_ to really learn some software tools.  Not to gain the superficial knowledge of how to get common tasks done, I'm talking about how to _really_ use the tools to prevent flaws from creeping into your code.  This also points to a hidden cost of switching tool sets.

It takes _years_ to learn how to write code that doesn't just work, but works well and is also maintainable.

It takes _years_ to learn when to walk away, take a break, take a stroll, to stop pounding the keyboard because you're not making any progress.  This is in direct opposition to that 100 hour a week work ethic, but it's a necessary skill - knowing when to walk away and still not give up. 

It takes _years_ to learn how to test properly.  Too often the agile "test early, test often" maxim demonstrates [Goodhardt's Law](https://en.wikipedia.org/wiki/Goodhart%27s_law), with a large number of tests all covering the same section of the code base.  There are also cases of developers simply coding unit tests to `return true`.

It takes _years_ to learn not to reinvent the wheel.  If there's an existing function or subroutine to do what you need, use it.  If it doesn't do quite what you need, maybe it needs maintenance, or enhancement, or maybe what you need can be implemented as a wrapper around it.

It takes _years_ to learn about the trade-offs that play into the decisions of how write a piece of code that reliably and securely does what it's supposed to do, performs well, and can be understood and maintained by people who aren't you.

By the time you get really good at software development, you're not young any more.  You've got an actual life, so you have good reasons not to work 60 or 80 or 100 hours a week.  You've gained the ability to look at a disaster unfolding and point to likely root causes.  You've acquired a more-than-superficial knowledge of design patterns and can spot anti-patterns in proposed designs.

By the time you get really good at software development, you know that extended overtime is just another take on the mythical man-month's axiom that throwing more people at a late project just makes it later.  Working extended overtime doesn't help either.

None of these things make you a more desirable staff member to management.  Most IT management mistakes activity for progress and your desire to leave and be with your family (or just get some downtime so you can think straight) is perceived as laziness.  Most IT management can't tell the difference between _good_ and _good enough._<sup>[2](#f02)</sup>

The fact that you're more productive is invisible.  That you can write code that is at once efficient, clear, secure, and does what is necessary is subsumed beneath the perception that by the time you're this old, you should be in management.  I mean, if you were any good, wouldn't that be your career goal?

Software development is supposed to look like a caffeine fueled frenetic party.  People in the middle of their career don't fit the image, and they cost too much.  I mean, we can hire two newly graduated youngsters for the price of one of those olds, and together they're almost half as productive, so... wait that doesn't add up.  Oh well, doesn't matter, we've got a _deadline!_  A _meaningless_ deadline!  _Another_ meaningless, arbitrary deadline!

One of the reasons software sucks is that developers get pushed out of coding before they have a chance to learn how to be _really_ good at it.  Because people think developers should be young and cheap and we instill in them a toxic culture that lacks essential mentoring and teaches them they should be _proud_ for having survived the latest wholly artificial unnecessary death march.

Quality costs.  Experience matters.

____________________________
<a name="f01">1</a> There are reasons things are the way they are.  Maybe even _good_ reasons.  [But they're probably not written down](https://github.com/cschneid-the-elder/rants/blob/master/recording-why.md).

<a name="f02">2</a> I've worked for good IT managers.  They're rare, and tend to accumulate excellent staff to work for them, in large part due to their being good IT managers.