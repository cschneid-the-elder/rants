The root cause of your frustration with mainframes: You do not have administrator rights on this box.

You are not allowed to install software and you only get to configure what an administrator _allows_ you to configure.

There are very good reasons for this situation, the most important of which is that _you are not to be trusted_.

You are not to be trusted because you want to change things without performing sufficient impact analysis.  You were just going to install something, weren't you?  Just to see what would happen?  Without regard to the other thousand or more people using that box?  What could possibly go wrong?  Did you just open up a security hole?  An attack vector?

If this seems pedantic, consider that the mainframe has been around for over half a century, running the business of organizations that _do not tolerate_ unscheduled downtime; do you think they haven't seen your like before?  "Let's try it and see what happens" is fine so long as you aren't acting in an administrator capacity.

The mainframe's legendary stability is in part due to the administrators' methodical, thoughtful, _careful_ approach to change.  Any change.  All change.  _Every single change._

Remember that all this software must play well together and it's the administrator's job to fix the problem(s) when some package(s) decide all the toys are theirs.  Maybe a particular version, release, or patch level of product X only plays well with a particular version, release, or patch level of product Y.  And maybe _there is no intersection_ between the versions that play well together of two or more products.

Performing a perfunctory Internet search to see if anyone else has found a problem with two or more packages is just not good enough, nor is skimming the TLDR section of a document, nor is checking your messages while a YouTube video plays in the background -- if you're an administrator then outages are simply unacceptable and you have to read the documentation, delving into the details, actually understanding the software ecosystem.  

Of course this isn't the production box on which the real business is conducted, it's a development box used by a whole bunch of your peers who are trying to do _their_ job, improving the lot of those who do the real business of the organization, which is pretty important too.  Yeah, I know, that's what _you're trying to do_, the difference is they're not risking stopping you from doing it by introducing instability into the infrastructure.

Development _is_ production for developers.

Configuration changes are similarly fraught with danger.  How much code has been written presuming the current configuration?  How will you find it all?

Customization for your project is sub-optimal because now you've _poof_ created a variation of the ecosystem, it's special, and thus requires special handling for impact analysis and software upgrades and thus you've _poof_ created work for the administrators.  In perpetuity.  Because you couldn't play well with the existing ecosystem.

Yes, it's the administrators' job to do impact analysis and upgrades, but they're a limited resource and quite frankly your willingness to argue and make a pest of yourself due to your lack of desire to work within the existing ecosystem is not sufficient reason to justify adding more administrators to the pool.

Your lack of administrator rights is unlikely to change, and it means part of your job is to know what is already installed, and who to talk to and how to ask them to install and configure what you believe your project requires.  Be prepared for pushback, because there is likely a comparable product already installed but that you rejected for reasons you must justify.  "I already know this other product" is not a justification.

If this all seems anti-DevOps, consider that [DevOps is not always appropriate](https://github.com/cschneid-the-elder/rants/blob/master/devops-raison-detat.md).  For some organizations, for some applications, stability eclipses delivery of new features.  Also consider that maybe, just maybe, DevOps is simply the latest in a long series of overhyped industry fads designed to sell training and consulting gigs.
