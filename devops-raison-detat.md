DevOps raison d'état<sup>[1](#f01)</sup> is obvious -- it's about control.

Humans find it distressing not to be in control.  Users want to be Developers.  Developers want to be DBAs.  DBAs want to be SysAdmins.  Everyone wants to be more in control of their work environment.  Eventually people might learn that that other job, the one they wish they had, that job consists of quite a bit more than just the part they see.  IT jobs are like icebergs that way.  This also works in the other direction, e.g. SysAdmins who have never been Developers tend to be surprised at all that is involved in a Developer's job.

So, under the guise of delivering something (_anything_, really) faster, we adopt this DevOps thing where the first requirement is to restructure the organization.  This shifts the conversation from the technical to the political (don't make that face, politics is just negotiation), thus taking power away from those darn techies who just _won't do as they're told._

One purpose for this reorganization is to remove barriers to _getting things done._  Unfortunately, [those barriers probably exist for a reason](https://github.com/cschneid-the-elder/rants/blob/master/bottlenecks-of-our-better-nature.md).

Now I'm going to write a dirty word.  Ready?  Here it is: __support__.  It's a terrible word, and many barriers are erected between people who want to get things done and the getting done of those things in the name of support.

I have been on both sides of this, and I understand the frustrations.

For the people charged with making your software ecosystem function smoothly, introducing change is something to be approached with fear and loathing and only after tons of research into all the different interactions and dependencies and whether the change is really necessary.  It's sort of the equivalent of developers' unit and integration testing only with all the modules being black boxes and if anything fails the business grinds to a halt and you get fired.

As much as the development staff insist they won't need any help with whatever new library or tool they wish to introduce, support staff know that it will fall on them to fix any incompatibilities, smooth any rough edges, and delve into every fussy configuration option.  This takes time and, well you've heard of the [tragedy of the commons?](https://en.wikipedia.org/wiki/Tragedy_of_the_commons)  Support staff are the commons.  They are a limited resource and every project wants 100% of their time.  You'll recognize them, they're the ones whose management agreed to have them scheduled to work 168 hours per week.

The development staff are just trying to deliver on time, within budget, and according to specs.  In order to do that, they've found a couple of products and a couple of libraries that will save weeks off their timeline<sup>[2](#f02)</sup>.  How hard could it be?  The answer, as it so often is, is _it depends._

It depends on whether or not your deadline is real or someone in authority invented it in a feat of procto-genesis.  It depends on whether or not the requirements leading to these products and libraries are requirements or the desire of a team member to pad their resume.  It depends on the cost of what's being requested.  It depends on the prerequisites of what's being requested -- we're fine as long as we upgrade the entire infrastructure software suite and reconfigure in a way that's incompatible with every other application system.

Application development seems to have devolved into the artifice of mercilessly stitching together tools and libraries into frankenmodules to be tortured into a lurching semblance of functionality.

Don't be _that_ team.  Don't be _that_ developer.  Don't be the cause of all the eye rolling.  Do the research.

Telling a support person that some random page on the Internet said you could do it this way is unlikely to garner sympathy for your position.

Meaning _really_ do the research.  No one has time for features that aren't _requirements_.  Sometimes the correct answer to a request from the business area is "no."

Be the project team that presents the need for a new tool or library in the context of the business requirement and the technical alternatives which have already been discussed with the support staff.

"I don't already know the existing tools that already satisfy those business requirements" is not a justification for bringing in a new toolset.

Reorganizing doesn't remove barriers.  DevOps doesn't solve a problem, it simply gives the project team the illusion of having more of a voice in the support equation -- but the project team isn't going to do the support.

Building secure, reliable, resilient systems isn't done by pasting together a bunch of disparate pieces of unknown provenance.  It's _work_, despite what you've read about coding boot camps in articles written by people who couldn't code their way out of a do loop.

It's _hard_ work, and reorganizing so the people responsible for security and reliability and resiliency have their voices silenced isn't doing the company any favors.  You just end up with insecure, unreliable, wobbly systems the support of which takes time away from building the next clot of systems you brought in DevOps for in the first place.

Bah.  Everyone seems to think that the stuff that isn't their job is easy, and easily understood.  DevOps reminds me of 1980s-era I-CASE tools that sought to speed up systems development by removing the possibility of typos in code.

____________________________
<a name="f01">1</a> I know what raison d'être means, this is [something else.](https://www.dictionary.com/browse/raison-d-etat)

<a name="f02">2</a> Also, let's talk about technical debt some time.
