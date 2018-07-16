---
title: City simulation
layout: post
categories:
  - Software
---
I've always been facinated by population simulation. Which, I recognize, is an odd thing for anyone to plant their interests. Here are some examples that I find facinating:

  * Sim City 2000 -- I grew up playing it. It uses high level stats to show demand between residential, commercial, and industrial sectors, then it simulates traffic based on roads size and zone demand. I think this is where the interest started.
  * Skyrim -- I recognize that they don't run full cities here, but this game helped me really appreciate a schedule for each NPC (non-player character) to follow to have even a semblance of a realistic city population. Characters in the marketplace each have a home where they sleep at night. They each walk to work in the morning, sand behind their stall, then go home. It's facinating.
  * Age of Empires 2 -- In AOE, the player controls the entire settlement as it grows from 4 villagers and a tent to a fortified city under siege. At first glance, it looks like it's all determined by the player, but each unit has a job to do (often with fallback options). Common walkways tend to appear, villagers will find new work when it's within a reasonable distance, soldiers can stand their ground or aggressively attack at first sight.

All that said, I have an idea for a whole city simulation that keeps coming back as a fun challenge. What if we could data-mine a whole city for statistical data and place a "person" in each home with a generated schedule, income, job that fit within the statistical model. Then we do the same for jobs, entertainment, medicine, etc, and simulate the movements of all the people in a city. The real difficulty in writing the software is that we'd be simulating a person's schedule. People are complicated and do a lot of things.

But if we could get past that hurdle and generate a model that fairly accurately reproduced the same road congestion conditions (same time and load), then we can change the map, run the simulation again, and see if the road conditions are better. Instead of guessing or just running standard statistical models at a road project, new bypass, light rail, etc, we could run a city simulation on it to see where the new bottlenecks appear.

It's possible that we could even bump the population up, build a new industry, company, park, or airport, and the simulation would give a good idea of what would happen once it's built. Probably. If it's done right.

Does everyone else have a "big problem" to which their brain keeps returning?