Modernization, or digital transformation by some definitions, of your application portfolio as a euphemism for "rewrite as microservices or APIs or whatnot" is an interesting concept.

In the old days, before the surface of the earth had cooled, I'm talking about back in the 1970s mind you, _ancient times_, IBM told their customers to write their applications in layers, or what we called tiers when client-server had newly crawled out of the primordial digital ooze.

 + User Interface, where screens or panels were displayed, data was solicited from a user, edited for syntax, and displayed.

 + Business Rules, where the actual business logic lived.  Is this license application valid?  Does it conform to laws, rules, and regulations?  Must the user be prompted for additional information?  And so forth.  This is the important layer, where tons of maintenance has been applied over the years.

 + Data Access, where DL/I or VSAM or BDAM or choose-your-DBMS calls lived, what today developers would call a persistence layer.  You swapped this out for SQL as you moved to DB2 as IBM recovered from their DL/I-is-for-OLTP and DB2-is-for-OLAP fugue.

The first layer invokes the second via a known interface, the second invokes the third with a known interface.  Likely these interfaces consist of data structures stored in copybooks or include members.  OO people will recognize this as an implementation of encapsulation, albeit in non-OO languages.

Well designed applications look like this, and this general design is conceptually familiar to most developers, regardless of language, paradigm, or platform.

It's also reusable, as you can, with a little bit of work on the plumbing, invoke the Business Rules from any language, paradigm, or platform that supports web services.  So, from pretty much anywhere.

Something we learned in the 1990s with the widespread acceptance of (followed by demand for) GUI applications was that, to the end user, the interface _is_ the system.  So being able to put a new coat of paint on the UI, whether it be webby or clientish, is important.  Don't rewrite your entire application just because skeumorphism has gone out of fashion; feel free to flatten the look, round the corners, skinny the fonts, tune the color palette, but please leave the business logic alone.

If you're looking at rewriting your application portfolio because it was originally written with the layers intertwingled, I urge you to consider that the safer approach is to detwingle the layers without incurring the risk of rewriting in a new language.  If you find you must rewrite because you want to replatform, that's a separate project.

Refactoring, rewriting, and replatforming as a single project is a sure way to become famous, but not in a _good_ way.

Be cautious in refactoring your Business Rules layer into microservices or APIs or what-have-you.  What may be possible to do in a technical sense may be impossible to do in a business sense.  The Business Rules layer looks like it does because it _reflects the business_ and _enforces business rules_, however inconvenient that may be for some snazzy new mobile interface.

Approach with fear and loathing refactoring the Data Access layer.  Unlike modern persistence layers that store whatever JSON and XML blobs of goo you throw at them and leave it to the developer to figure out the mess with XQL embedded in SQL and other abominations, classic database structures _reflect the business_ and _enforce business rules_.

Safety first.  Let's not disrupt the business simply because we like semicolons and curly braces and the latest multilayer frameworks freshly downloaded from dodgy websites.  Particularly when your well-written applications don't need rewriting or replatforming _at all_, just a new coat of paint on the UI or the addition of a new layer hosted elsewhere that makes use of the Business Rules layer as a service.
