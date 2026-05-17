---
layout: post
title: "High voltage, low patience"
description: "Ordered a Kelly motor controller, got offered import fraud, declined. Broke a serial adapter. Programmed the controller anyway. Got half the HV bench wired before running out of copper connectors and steam."
category: vw
tags: [vw, ev-conversion, high-voltage]
---

The HV bench test is finally happening. I've got most of the components I need, half of them are wired up, and getting to this point was more of an adventure than it had any right to be.

<!-- more -->

## The Kelly controller saga

My first attempt to order the Kelly motor controller was through a Canadian supplier. A day or two after I placed the order, they emailed me to say they weren't working with American customers anymore — tariffs had made it too complicated. They refunded me, no drama.

I found one other supplier and placed a second order. Not long after, I got a message from them — not through any official channel, just a side message — letting me know that while tariffs were running around 52%, they could mark the package value at ~$100 instead of the actual ~$600. I'd Venmo them ~$50 to cover the reduced tariff and we'd all be better off.

I said no. I'm not getting fined or arrested over a hobby car. I offered to pay $318 through normal channels, they accepted, and that was that.

It's just frustrating that this is the situation American hobbyists are in right now. Not much I can do about it except refuse to participate in the sketchy parts.

## What's on the bench

With the controller finally on its way, I've got a solid lineup of HV components ready for the bench test:

- Kelly motor controller
- High-voltage contactor
- HV fuse
- HV cable
- Current sensor (this one came in earlier)
- Prius accelerator pedal (a well-documented donor part that shows up in EV conversions everywhere)

![Kelly motor controller](https://lh3.googleusercontent.com/pw/AP1GczMjMQscaBAKNMyZO9_-cZWW7-jCpz7JnXLWBDeEa9nV3yUkE2P-wf-B5cBi8XJHFltFjADMQw3Y-gzZhVda3ryqK2-TesauwHQ6ggdgGZbCUUvaHOMWf2Pkbr7_-rfNuEldI6Zg0EyhDzBTKMDJ-MgmmQ=w1918-h1444-s-no-gm?authuser=0)

The whole point of the bench test is to get everything working together before a single wire goes through the chassis. If there's a problem with the wiring or a component is behaving unexpectedly, I'd much rather find out on the workbench than buried inside a 50-year-old car.

## Programming the controller

Before I could wire anything up, I needed to configure the Kelly controller, which requires a serial connection to a laptop. I bought a serial-to-USB adapter on Amazon.

The connector was obviously the wrong form factor — it wouldn't fit. So I pulled the shielding off with pliers, which came off way more easily than it had any right to, and left it like that.

![Serial connector with shielding removed](https://lh3.googleusercontent.com/pw/AP1GczPFHD1aihCDvRXp1jciARQ2_vrpdR5j1n97mdU5vut1cBzoeIHoJvUElRU7SegJcV1-26SEepT6bQZ0muTzrEpWJBktGN7km00_e7tUfvY1tORrNaZwIuU6MuIp1GKg6PSVQBkXWm84bTtuYi3SPrQ3uA=w1524-h2024-s-no-gm?authuser=0)

It connected. The controller is configured and ready to go.

![Kelly controller glowing during programming](https://lh3.googleusercontent.com/pw/AP1GczOhe5EItl9EXwQyokkJMeETJVXkKjya_Q2ydj190wrDG6umlPM2b2xgfGw82UDbCTZpbW_IHdyf1mNPjPTV9z1tA52apgLR3eJT20NgwlAbvFZ-vZgI-pN5teD1nxV60wtttixRy2WQwmd8J49gob9mtQ=w1918-h1444-s-no-gm?authuser=0)

## Today's wiring

Today I screwed down the HV components and started connecting things. The first real HV cable went in as a jumper directly on the motor, which felt like a meaningful step after months of sourcing parts and reading documentation.

![First HV cable as a jumper on the motor](https://lh3.googleusercontent.com/pw/AP1GczO3dsErNRagb4BzQ11r1vx8EvX86TyGgdr9VKXdPDPkfi7UVWQDSep2356kAtxItjSpjHF6iirOPzznmYXhh0IT6En_-acPov4WmzVketshsTvoknuAY7CXT8ejEjFNLSkUtbFVjj2W2vD-da4Y8LCN5A=w1918-h1444-s-no-gm?authuser=0)

I got about halfway through before I ran out of copper ring connectors and, honestly, stamina. This kind of work takes a lot of focus — you're constantly thinking about polarity, routing, what connects where and in what order — and there's a point where you start making mistakes if you keep pushing. I hit that point and called it.

![HV system with several connected pieces](https://lh3.googleusercontent.com/pw/AP1GczON1A8JqhMq4cGYWuaPPTQKskhZqtB34jYnWKqjPWJlOPGu0fGu7UN3KXZrpVZnoDB1LiZix6aUdGVxxqX7JcWJVuXi15qoiF9opnrlaOXFVunAL1nQmi1k1QMpbpR4H7xxTi8VN_MpBvKZb2hbgtSW0g=w1918-h1444-s-no-gm?authuser=0)

Half wired is still further than I was this morning.

## The missing piece

The HV bench isn't the only thing I've been working on. Back in March I mentioned that the adapter plate and coupler setup for the WarP9 motor wasn't adding up — I wasn't sure I had the right parts to physically connect the motor to the crankshaft.

I started calling machine shops. Three different shops in the area, and all three of them pointed me to the same machinist. He was terse on the phone, which I actually took as a good sign — he didn't have time for small talk because he knew what he was doing.

I've ordered both sides of the coupler, but I still need to take some measurements before I can bring anything to him. If he can manufacture the connecting piece, the WarP9 finally has a path to the drivetrain. That's a significant if, but it's the most promising lead I've had on this problem since March.

## What's next

Copper ring connectors are on order so I can finish the bench wiring. The 6-pin harness for the Prius pedal should be here tomorrow, which will help with getting that part of the system tested. Once everything's connected, I can do the first real power-on test of the full HV setup — BMS, contactor, controller and motor all running together.

I also need to get those measurements so I can get to the machinist.

And yes, the Android Auto ignition wire and DIN latch are still on the list. They'll get done eventually. Probably.

[All the VW EV Conversion posts](/vw-ev-conversion)
