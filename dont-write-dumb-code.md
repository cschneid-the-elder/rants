Don't write dumb code.  That's what Tom Peltin said comprised the entirety of his coding standards when he hired me in 1989.

He said he'd sat down and tried to come up with a set of coding standards some years prior, and every effort he'd made ended up being a style guide.  So he settled on "Don't write dumb code."

I've told people that story and had them scoff, point their chin at the ceiling, and mistaking cynicism for sophistication contemptuously ask, "What does that even mean?"  They tended to write dumb code, if they wrote code at all.  The disrespect which which some IT staff regard the programmers who write the very code on which their organization relies is astounding.

Dumb code demonstrates a lack of regard for the maintainer on the part of the author; where there's an easier, clearer way of accomplishing a task and that is the path not taken either actively, i.e. _on purpose_, or passively, i.e. through apathy.

Dumb code is gleefully unclear, making use of obscure parts of the language not because they provide a better mechanism for solving the problem at hand but only because the _obscurity is seen as a goal_ in and of itself.

Dumb code is an obvious attempt at job security.  It should result in the opposite.

Dumb code is a land mine, waiting to be stepped upon by a system upgrade, application maintenance, or enhancement.  It's going to cost time and money and blood pressure credits so why put up with it?

This is _not_ to suggest that advanced features never be used.  The idea that features not immediately comprehensible to a novice should be banned results in the dumbing down of a technical ecosystem to the extent that new development becomes well-nigh impossible.  Also, advanced features are _cool_.

If you get done writing something and think it's ugly, refactor it, rewrite it, in the names of Babbage and Lovelace _take some pride in your code_.  Sometimes it is necessary to push back against TPTB and their deadline fetish in order to prevent future pain and suffering on the part of the organization, and more importantly on the part of whomever might maintain your code.  The sanity you preserve may be your own.

Managers that insist on shipping the first thing their developers get to work do not have the best interests of the organization in mind.  _Their_ managers should take note of this disregard.

The Perl mantra is, "There is more than one way to do it," (TIMTOWTDI).  Larry Wall, who invented Perl, [has been quoted as saying](https://www.azquotes.com/quote/923764?ref=perl), "Perl is designed to give you several ways to do anything, so consider picking the most readable one."

I have been in code walkthroughs where veterans say, "Look at this, this is how code should be written, it's clear."  We should all want to hear this when our code is reviewed.  _That's_ a proper goal.

Expect better, both of yourself and your peers.
