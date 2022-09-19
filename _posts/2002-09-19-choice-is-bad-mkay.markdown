---
layout: post
title:  "Choice is great, but also how you get ants"
categories: tech 
---

## TLDR

Choice fosters exploration and growth by being inefficient. Growth leads to increased experience. Increased experience brings clarity. Clarity helps eliminate choice which leads to greater overall outcomes and a new set of choices to consider.

Nature teaches us this. I imagine this largely accounts for [neuroplasticity](https://en.wikipedia.org/wiki/Neuroplasticity), but I'm way out of my lane on that one. We should embrace it. My feeling is that as a specices the reason kids can successfully learn, is the same reason young adults can challenge norms and look for new areas of growth, is the same reason elder folks can impart wisdom, and is why we humans are what we are. As you mature, impart your domain wisdom and remove choice that leads to poor outcomes, while fostering the next wave of folks to improve upon the better choices we have reached through experience.

## Background

I often cite that my happy place is "building basements". What I mean is that I tend to gravitate toward building lower-level components that themselves facilitate higher-level and eventually user-facing components. I don't know why this is, I have just chosen not to fight it. As I matured in my career, I also noticed I was spending more time thinking about patterns and looking for ways to facilitate others to build components in my basements. In other words, building foundations or frameworks more than just features. This seems like the natural evolution of one's career, or at least we basement builders.

Just like building an API, building an extensible framework requires a lot of thought about today's requirements and trying to anticipate tomorrow's requirements as well. The "user" in these scenarios tends to be other developers, which is great because no one has greater empathy and understanding of this "user" than other developers. The problem, is that one's empathy for this user is so great that it is difficult to avoid giving this user all the tools she may want or need. And here is the problem: "Choice is great, but also how you get ants".

## Examples

I have nothing but personal experience and anecdotal observation to add, but I shall attempt some examples to make my point or prove my ignorance.

### Tech Example: Managed Endpoint Extensions

Years ago, at my current job [Tanium](https://tanium.com), I was one of several early devs who were using the primitives of our platform (we call them Sensors and Actions), to discover ways to extend the feature set of our agent and to explore the world of products on top of this platform. We were rapidly growing our capability set on top of our highly scalable endpoint management system and finding our way like any high-growth software company. We were organically trying different technologies, different conventions, balancing between shared code vs shared patterns, and it was awesome! We moved fast. We delivered value quickly. I recall being on customer calls and responding to questions like "That's cool, but when can I actually have it?" and the answer being "How is next week?". As one might imagine though, this also leads to divergent solutions, divergent user and support experiences, and a lot of technical debt. Having so many ways to solve problems gave us huge initial benefits and also gave us ants.

The "ants" in this case is really the debt. New developers are lost because there are so many ways the same things are done. New initiatives to rollout a common change take forever for the same reason. Supporting so many different solutions is a huge burden on developers and your field people. Eventually the very thing that made us fast made us slow.

So around 2018 I took a step back and tried to find a solution that would consolidate everything we learned (the good and the bad), look for patterns, and build an ecosystem for our agent that would help us scale more effectively. My hope was to take away choice and give developers a safe and easy mechanism to extend within the ecosystem and remove the need to solve common problems over and over. The good news is it was successful. The bad news is we got new ants.

One concrete example is that I wanted to address at the time was the need for resource monitoring and throttling by introducing an asynchronous work scheduler and strongly encouraging all background work to choke through this mechanism. It works great...when you use it. The solution removes the need for developers to care about such things and yet provides the safety we promise our customers when it's used. That's a win! The problem is that in most cases, this turned out to be too much choice. The folly was in the "strongly encourage" and opt-in mechanism for the system.

If I could go back, I would keep this same foundation and then iterate again to remove the choice of scheduling your own work as a developer for most feature use cases and still expose the lower-level scheduling for the more primitive shared components. I would probably do this by asking "what makes work happen?", to which my answer is "some event" and would probably force extensions to only be able to perform work as a response to some event and thus force them into a managed work scheduler.

### Life Example: Food

10 pages on a menu is awesome, right? I can probably find anything I want! I probably will also have a lot of anxiety about it, second guess my choices, and likely diminish my experience because of the anxiety and fear of missing out on what I didn't choose. It will also take me a lot of time to decide on something. My personal experience tends to increase when the restaurant's chef chooses for me by giving me few options. One of the best ways to get a correct wine pairing is to ask them to choose for you. (I'll concede, you might also get whatever the bartender is trying to finish off so the bottle doesn't get thrown out, but let's give them the benefit of the doubt).

### Observed Example: Photographers providing galleries

My wife, Lindsay, runs a [photography business](https://www.lindsayaikmanphoto.com/). She is always looking to balance the general problem, especially when she was shooting weddings where the volume of pictures is just so high, of choice. Give the client hundreds of pictures in a gallery, they are overwhelmed. Give them too few, and they may not find what they need or want. More often then not though, they tend to prefer that she reduces the choices down to something manageable. 

Similarly, she is starting to optimize for the packages of physical products toward pre-chosen wall arragenements and albums, reducing down from a large set of ala-carte choices. Clients respond well do this. I've heard friends say similarly that when galleries have too many photos, they just don't know what to choose and often don't feel as good about their choice.

### Observed Example: Kids

Above in the TLDR, I presume to suggest a link between how we have evolved as a species and the cost and benefit of choice. As a parent, I witness this. Kids need to fail, but the sandbox of failure needs to be safe. My experiences and the combined experiences of our species have eliminated choices like playing near the edge of a cliff, attempting to eat fire, or poking a large animal with a stick. I am really glad that some predecessor had the choice to poke other animals and I'm also really glad that the ones who did and paid for it by getting killed allowed others to learn not to do that. (I'm totally contriving this illustrative example....probably).

My children will hoepfully stand on the foundation my generation is providing, which was built on our shared elimination of inefficient or sub-optimal choices, and be introduced to new challenges and problems which require us to eliminate more of the sub-optimal ones.

## Conclusion: Encourage an easy layer. Maybe expose a harder one.

Back to tech. My current thinking tends to now lean towards a balance of choice elimination and capability exposition. (duh?) The way I do this is to separate "how would I use this?" from "how would someone new to this capability want to use this?". One may find the answers are often quite different and yet inherently layered. The lower-level capabilities that facilitate the higher-level ones may be beneficial to advanced users' needs, but often give the majority too much choice. If this were not true, we wouldn't be exploring a higher-level, less-choice layer in the first place.

This should be obvious. We have evolved from raw socket operations to mature network stacks to high level lanugaes and tools that let you interact with remote services in a single line of code. That is evolution of feature by elimination of choice! However, we never took away the lower level APIs, we just don't use them directly as much.

Also, our naturual inclination is to over-pivot on the lowest common denominator as our wisdom compels us to not just build for today, but to leave ourselves room for tomorrow. This is good, but I would encourage you to make that an implementation detail of the framework, not the user-facing interface of your framework. Put another way, build the guts of your framework to be extensible to you, but build your framework's API to be extensible to your consumer given the patterns you see today.
