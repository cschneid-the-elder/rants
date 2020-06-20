In the noughties, my employing organization's management would periodically declare mainframe application costs to be too high and that _something must be done,_ sometimes leading to a demonstration of the Politician's Syllogism<sup>[1](#f01)</sup>. 

My initial response was to run a report of the most costly batch jobs and see what could be done to tune them.  I was able to empirically prove there were instances where DB2 joins of massive tables could be done more efficiently by unloading the data to flat files and doing the equivalent match-merge operation.  There were the inevitable instances of COBOL arithmetic being done with USAGE DISPLAY fields.  There were tiny DB2 "code tables" being reread for hundreds of thousands of input records instead of being cached in Working-Storage tables and searched there.

This was not what management was looking for.  Management was looking for how to lower costs _without changing the applications._  So, lower costs without tuning.

Well, why didn't they say so in the first place, I thought.  That's easy, we'll just add `PARM='LOWER_CPU_COST=YES'` to all the batch jobs<sup>[2](#f02)</sup>.

Of course, they didn't tell me that right away.  This revelation that people in a position to make decisions actually thought application costs could be reduced without tuning said applications only came to light after a couple of rounds of attempted cost cutting.

Now, there _are_ some [things you can do](https://github.com/cschneid-the-elder/rants/blob/master/apps-tuning-with-le.md) to reduce application costs without changing either the source code or even recompiling.

But the notion that you can seriously cut costs without changing or recompiling your code is a fantasy.  

Yes, IBM now has their Automatic Binary Optimizer, but it _costs_ money and you're trying to _save_ money.  Also, it's the moral equivalent of recompiling.

Yes, IBM's latest COBOL compiler generates more efficient code but you'll have to thoroughly test your applications because programmers have been taking advantage of "it just happens to work" compiler behaviors for three decades.

 > Has anyone in your IT shop noticed that there's this great resistance to a project to recompile and thoroughly test everything thus benefitting _now_ from the latest technology (both compiler and hardware), but the idea that instead of getting all that work out of the way at once you're going to be doing that project from now until the end of time is all fine and good?  Delaying that work means you're not taking advantage of your mainframe's hardware.  It's just odd to me that people who say they want to save money work so hard to make sure they don't.

So what's the secret?  What's the one weird trick that will save you money?

__Actually tune your applications.__

 + Use an application profiler, if you've got one, and fix the hot spots in your code
 + Absent an application profiler, use SMF and/or chargeback data to identify your most expensive applications and have staff with a head for tuning give them a working-over with IEBIBALL
 + Refactor your code where necessary, incorporating more efficient algorithms
 + Recompile with the latest compilers; do the migration ASAP
 + Investigate in-memory processing
 + Recognize that the price of some forms of tuning is that you must revisit them as upgrades are made to infrastructure

There is no secret, there is no trick, there is no magic charm or incantation or pixie dust that will reduce the cost of your applications with no investment of time and effort on your part.

It's work.  Hire smart people, listen to them when they tell you what is necessary, and otherwise stay out of their way<sup>[3](#f03)</sup>.

____________________________
<a name="f01">1</a> [Thankfully not very often.](https://en.wikipedia.org/wiki/Politician%27s_syllogism)

<a name="f02">2</a> At this point a colleague and I suggested the organization stop paying $US six figures per year to Microsoft and use FOSS instead.  This was _not_ well received.

<a name="f03">3</a> Or maybe _that's_ the one weird trick.
