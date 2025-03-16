## Context
I recently purchased a ThinkPad X280 as I've missed having a laptop and would like to avoid spending most of my life strapped to a desk chair as I undertake some work on the side.

As an aside - I adore this laptop. The **sub**-1080p 12 inch display is very charming, the 16GB of RAM and i7 inside of it is doing the job and this is especially true as we get to talking about the software this device is running.
![[photo_2025-03-03_17-22-19.jpg]]
I've been using [Nobara](https://nobaraproject.org/) on my desktop, and have loved it since installing it. Nobara is self described as trying to *"offer a better gaming, streaming, and content creation experience out of the box"* - three things that this machine is not trying to do.

I actually learnt of my choice [Aurora](https://getaurora.dev/en) as well as the great work done by its maintainers Universal Blue through [Bazzite](https://bazzite.gg/). Bazzite's been doing the rounds recently as the closest thing to Steam OS currently available to install whilst we wait for an official stable release from Valve.
Where Bazzite appeals to the sweats - Aurora instead advertises itself as a productivity oriented OS especially catering to developers.

Universal Blue as a company have a very captivating vision with their lineup of images - they're all in on Fedora Atomic based images with Bazzite and Aurora being examples of how you can tailor these images to specific use cases.

I've been using Aurora on my laptop for around a month now. I could still be in a honeymoon period with this OS but I've had an overwhelmingly positive experience with it.
## The best way to use a computer
I'll come out of the gate saying that - I think there is an argument here that this is how personal computing should be. 
Universal Blue make it very apparent on their home page what they're trying build: *"the reliability of a Chromebook, but with the flexibility and power of a traditional Linux desktop"* (I'm not a Universal Blue sleeper agent by the way, it's refreshing to see a company do something to make something better than the status quo).

The best way I've found to describe the user experience considerations of immutable distros is *"everything adjusted outside the home directory is wiped on restart"*. I feel this is the uphill battle that these operating systems have - the concept is scary on paper. Even as I use this laptop it's taken me a while to figure out when this device actually updates, or what I can and can't do. I say this all within the context of myself being a developer - someone who naturally wants to know how this works and enjoys mucking with the inner workings. For the standard end user, the caveats of how immutable distros operate pale in comparison to the main blockers for broader Linux adoption.
If I were to install Aurora on my Mum's desktop - I doubt she'd ever be concerned with the fact her system is essentially recreated on boot every time and it certainly would pale in comparison to much bigger blockers to Linux adoption such as *"how do I install Word on this"*.

I could imagine if this concept took off in the broader corporate environment it would be a game changer. I'd be happy to relinquish my admin access if my work device came with a copy of Aurora installed - as I'll get into later if the operating system actually caters for a way of working that is so reliant on containerisation over making modifications to the base system you realise how little you actually need super user privileges to your own device. 

This does not come at a trade off of control - my Aurora installation may not allow me to break it but thanks to deep integration with [Distrobox](https://distrobox.it/) I still am able to fuck up my Linux installation as I'm prone to doing **but** within the safety of a container.

Before I landed on using my X280 to remote into my desktop for development purposes, I found the flow of using containers to manage development environments to be very satisfying. The tooling is there, as much as Microsoft's consumer products and services continue to destroy any good faith I had for them you can't argue that the [Dev Containers](https://containers.dev/) spec isn't solid. I was able to have a fully functional .NET Development environment and accompanying Postgres database running off this laptop - all without ever needing super user privileges or installing `dnf` packages.

There were times where I felt it was more of a headache than it was worth - I don't think this is an Immutable Distro problem and more a mindset shift that's required with any form of container reliant workload. It might be easier to just drop some web app files onto a server and put it behind a reverse proxy when compared to the process of getting your application containerised and deployed correctly *but* I don't think that's ever been the selling point of this paradigm. The small amount of effort put upfront results in consistent incremental improvements over the alternatives long term, that's why we do it. 

All this to say that yes - immutable operating systems on paper may sound a little weird but like developers like the team at Universal Blue cook.

