---
layout: post
title: "Math Isn't Fun: DiffEQs and Zombies"
date: 2014-12-31 9:00
authors: [logan]
description: For a final project in a multivariable calculus and differential equations class, two of us worked on a Python zombie game featuring famous DiffEQs like the 2D heat transfer equations and the SIR pathogen model. The most valuable lesson we learned? Math isn't fun.
tags: [math, python]
---

  Last semester, for our big final project in our required differential equations class, Dakota and I coded a zombie game. 

  At this point, understandably, those readers who went to schools with things like "exams" and "textbooks" may have a few questions. Let me try to head those off at the pass. 

  * "Wait. Your math class had a final project?"

  Yes. Olin College, the academic venue of choice for this fine blog's young authors, is proudly... nontraditional. Institutionally, Olin would rather let students learn by doing than by reading or listening, and this preference shines through in classes from Software Design (where the do-learn paradigm makes a lot of sense) to Multivariable Calculus and Differential Equations (where I might've appreciated an occasional quiz). No, there was not a real final exam, nor was there ever a test.

  * "You _and_ Dakota? Why are so many of the posts on this blog about the authors working together?"

  For one thing, a key part of the Olin experience is learning to work in teams. Personally, I'm pretty happy about that, since I figure I'll be spending a big chunk of my engineering career doing group work. For two thing, it makes sense to write on our shared internet blog about our shared real-life work. And as for why the three of us seem to wind up partnered so often: Dakota and I are roommates, and Dimitar's our next door neighbor. Sheer laziness, is basically what I'm saying.

  * "A zombie game? What on Earth do zombies have to do with differential equations?"

  Ah, but this wasn't just any zombie game. This was a _sophisticated_ zombie game.

{:.center}
![screencap of zombie game]({{site.url}}/assets/zombies.JPG){: .image }

  Figuring that we should at least pay lip service to the actual subject at hand, Dakota and I tried to make sure our game was mostly a differential equation visualizer. Sure, we coded in a couple forms of user input - "air strikes" and "infantry insertions" - but the real point of the project was to watch famous differential equations interact on randomly generated 2-D planes. At least, that's what we told ourselves. Deep down, I think we really just wanted to craft something cool, with one foot in the realm of DiffEQs and the other in the land of game design.

  And by 10 PM on the night before the project was due, we had a pretty solid prototype together. Our code randomly generated a continent, seeded it with people and zombies, and then let the differential equations run wild. There were a few bugs (check out the floating-point fractional zombies in the screencap above, for one), but we had a reasonably well balanced, good-looking game that we thought was pretty fun to play. 
  
  There was just one big problem: the math wasn't legit. 
  
  Making sure to commit our last good version to Git, Dakota and I began work on improving the mathematical legitimacy of our model. I updated the zombies' inter-tile movement algorithm to match the two-dimensional heat transfer equations; he patched the intra-tile zombie/human combat to more closely resemble the traditional SIR model of disease transmission. After a couple hours spent head-bangingly hunting down a nasty bug in the SIR update method that would double-count zombies chosen by the diffusion equations to move down or right, we decided we'd made things as mathematically reasonable as we could and tried out the new version of the game. 

  It sucked. 

{:.center}
![boring screencap of zombie game]({{site.url}}/assets/boring-zombies.png){: .image }

  On the one hand, sure, it was hypothetically a better model of the zombie apocalypse. But _who cares_? The SIR model is deeply flawed, and I'm pretty sure that real zombies wouldn't move across a continent the same way heat flows through a metal sheet. (We'll leave aside for now the question of why anyone would need an accurate zombie apocalypse model in the first place.) And by rewriting our game's core mechanics to match them up with real-world differential equations, we'd compromised the delicate balance that made it fun to play in the first place. Instead of behaving differently on different continents, the newly nerdy zombies now more or less just ignored our maps' terrain features. User input was meaningless in the face of the more powerful new DiffEQs, which could nullify any "air strikes" or "insertions" in seconds. The program reached the same end condition in every single test. We'd improved our model, but broken our game.

  In the end, the whole all-nighter we pulled to make our simulator more "realistic" and "mathematically legitimate" just made it less fun to play. In the context of the final project assignment, this was perhaps not a great loss, but it was a big realization for me nonetheless. What I hadn't understood before - and what I do now - is that math isn't fun.
  Think about it. Name a single popular video game with a strong basis in mathematical modeling work. Even Papers Please, more or less a glorified filing simulator, is set at an immigration checkpoint where every tenth passerby is a terrorist. Games like Goat Simulator and Surgeon Simulator are fun _because_ their models are broken messes. Why this tendency away from realism in gaming? Because the set of things human brains find "interesting" and "fun" is very different from the set of things that reality finds "accurate" - which is _the whole reason video games exist in the first place_. 
  
  In retrospect, of course making a zombie game grounded in actual mathematics was a terrible idea. If the interactions between the SIR model and the heat transfer equations in the two-dimensional domain were fun, we'd all be math professors. And, speaking of math professors - I bet ours would find it a little galling that one of the biggest lessons learned from our final project was about game design.
  
  But I guess that's just what happens when you go to school at Olin. 
