I was recently pointed at an article in [Enterprise Executive 2020 issue 2 page 18](https://www.mydigitalpublication.com/publication/?i=657478&ver=html5&p=22).  I don't know how long that link will live, so here's the author's (Mark Schettenhelm) words which set me off.

 > Customers have little loyalty and little tolerance for an application that doesn't fit their needs.  They have no problem taking their business elsewhere if they're not satisfied.  Our development teams need to understand that the environment has changed, the pace has quickened.  We cannot be left behind!

 > Knowing this, we have to rethink how we look at deadlines.  Instead of a set date when a particular project must be done , we have to consider each day as a deadline for providing value to our customers and keeping pace with their evolving needs.

The author of the article makes some very good points<sup>[1](#f01)</sup>, but the overarching point about deadlines is misapplied.  Just because something works doesn't mean it works well. Implementing the first thing you get to work is not necessarily a good idea.  Yet this is behavior encouraged by artificial deadlines of the sort created by the author of the article, who insists IT staff must regard every day as a deadline.

[I've made this point before](https://github.com/cschneid-the-elder/rants/blob/master/why-software-sucks-000.md), but it bears repeating.  Good code - reliable, efficient, maintainable code - is produced by IT staff with the training, talent, and time to reflect on their design and implementation decisions, not in some panicked marathon coding session fueled by caffein and junk food perpetrated by managers who sincerely believe that their staff require urgency to produce something, anything really, so long as a delivery date is met.

While the perfect may be the enemy of the good, terrible code produced simply to hit a target is the enemy of stability, efficiency, and future (perhaps actual, real) deadlines because it causes production issues.  Those fickle customers also require that your code actually _work_.  Don't tell me you've got unit tests to take care of that, we all know how many of those simply `return true`.

And those who insist premature optimization is the root of all evil _really_ need to pay attention to the rest of that quote...

 > We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%.<sup>[2](#f02)</sup>

...and the other comment Knuth made about optimization...

 > In established engineering disciplines a 12% improvement, easily obtained, is never considered marginal and I believe the same viewpoint should prevail in software engineering.<sup>[3](#f03)</sup>

Of course your team has to deliver something; noodling away at the code forever has never been an option and suggesting that is simply a straw man.  The disagreement here is over _artificial_ deadlines, the idea that "good enough" is dictated by the calendar and not by user experience with your code.


____________________________
<a name="f01">1</a> Organizations must train their IT staff, applications must provide for multiple UIs and APIs, IT staff need proper tools to do their jobs - all good stuff, no argument from me and kudos to Mark Schettenhelm for saying something that needs saying.

<a name="f02">2</a> Knuth, Donald (December 1974). "Structured Programming with go to Statements". ACM Computing Surveys. 6 (4): 268. [CiteSeerX 10.1.1.103.6084](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.103.6084)

<a name="f03">3</a> ibid.
