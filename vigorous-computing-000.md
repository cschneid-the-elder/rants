Now that the cloud model has been accepted as an industry standard, we can move past convincing stodgy IT departments to give up control of their organizations' data and the processing thereof and procede beyond agile computing to _vigorous computing_.

And what is vigorous computing?  Vigorous computing is characterized by meta-cloud thinking, a cloud of clouds, a _thundercloud_ if you will.

The thundercloud concept is, at its heart, an exercise in reliability and resiliency.  Where a cloud services provider can certainly increase reliability and resiliency by spreading your service across availability regions, true reliability and resiliency is attained by splintering the services you require _across cloud providers_.  Divide and conquer, just as history teaches us.

A new open source offering called QAM (short for Qui Adsunt Multos) can be configured to manage unattended failover between all the major cloud providers.  In addition, QAM implements other vigorous computing paradigms including CFTP (Continuous Failover Testing in Production).

CFTP is a configuration option which eliminates the guesswork that comes with failover.  We all know the pain point of failover is testing; well, QAM, properly configured, is continuously testing your failover capability by failing over between your contracted cloud providers on an irregular basis - _without warning!_

Unlike traditional failover testing, which is scheduled and takes place in a test environment with a simulated workload, by testing failover in a production environment you will be assured that that your failover process actually works where it counts, in production.  And by testing failover continuously, failover ceases to be the exception - it's just a normal event.

While your competitors are worrying about whether or not their cloud provider can keep up with demand, you can check in with I^2 (the QAM Introspection Interface) and see you've failed over between providers dozens of times _today,_ without difficulty.

How does this work?  Put simply, it's clouds all the way down.  QAM is a fully cloud-enabled and cloud-ready application itself.  An instance is running on each of your cloud providers' infrastructure, and each instance communicates with each other instance.  Collaboratively, using a machine learning algorithm, these instances decide when to fail over and to which provider.

We call this machine learning algorithm the orchiographer - a portmanteau of orchestrator and choreographer, because it directs both the orchestra (the cloud provider) and the dancers (your applications) - and you can rest assured it's been trained on a broad set of dozens of different scenarios for failover.

And the magic is that each failover that occurs in your production environment will feed another scenario into the training dataset, customizing your instance of the orchiographer to more precisely control your failovers.  So the orchiographer is also being tested _and improved_ in production!

Now, you're probably wondering about cost.  QAM itself costs nothing, but you will have to have one dedicated cluster running on each providers' infrastructure to run it.  Beyond that, your application portfolio is only running on one providers' infrastructure at any one time, so with the elasticity of cloud provisioning your costs are no more than roughly the mean of all your cloud providers.  And since I^2 provides the capability to fail over to any competitor whenever you choose, you are in a much stronger bargaining position when it comes to negotiating rates.  Don't like one provider's pricing?  Go elsewhere, and the more people who use QAM (again, it's free) the more people who are in a position to do the same.  You'll see those rates come down right quick.

Your data.  The best has been saved for last.  You have options...

 + Keep a copy of your data on each of your cloud providers' infrastructure.  Keep them in sync with any of the available open source packages.
 + Keep one copy of your data on whichever cloud providers' infrastructure your applications are currently failed over to.  QAM can optionally copy your data when spinning up infrastructure during failover.
 + Allow us to manage your data with the most thoroughly tested hypervisor running on the most securable and most reliable encryption-everywhere infrastructure (seven nines availability!).

This is the promise of cloud that we all dreamed of more than a decade ago, finally delivered by vigorous computing and _the thundercloud!_

__________________________________
_I have a visceral fear that the preceding attempt at humor will instead be seen as a goal._