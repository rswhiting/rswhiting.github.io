---
layout: post
title: "And yet it moves"
description: "Mapped the throttle pedal by hand, found a missing safety part, talked myself out of another one and spun the WarP9 for the first time."
category: Blog
tags: [vw, ev-conversion, high-voltage]
---

The motor spun. The Warp Drive (WarP9) turned on the bench because I pressed a pedal.

It was monumental and mundane at the same time. Months of parts, diagrams and waiting on shipments led to this moment. What I actually saw was a bare shaft spinning for a few seconds and slowing to a stop. That was it.

Getting there took a lot of small sessions. Some were at the bench. More were online, searching for parts and reading manuals. Along the way I found one part I didn't know I needed and dropped one I thought I did.

<!-- more -->

## Two diagrams, zero agreement

The Prius accelerator pedal has six wires. I had two diagrams telling me which wire did what. They disagreed.

So I stopped trusting either one. I put 5 volts from a bench supply across pairs of wires and probed the rest with a multimeter while pressing the pedal by hand. One group of three wires did nothing useful. One wire sat at 5 volts no matter where the pedal was. The other group gave a clean sweep: 1.58 volts released, 4.53 volts floored.

The pedal has two sensors inside for redundancy. I only need one. The second can stay a mystery for now.

With the wiring sorted, the controller still threw a throttle error at power-up. Its defaults expected a different voltage range. Once I gave it the real numbers, the error went away.

It also threw a low-voltage error. That one I expected. The controller watches the main battery input, and the battery wasn't connected yet.

![pedal wired to the controller](https://lh3.googleusercontent.com/pw/AP1GczOeFkcF2i6T18KYC-wW62pFATv--7lps9UCMHPEdkDMpbhnJnbC4D_BdpueueH3HpFpvplHVKQMb8Aq2Wj5kTGtS1JaF-gR9yBfRZwBNQXiTDMkZD3P72noIgiUhtWIkj86PTa9cBca_A9YctV4ND41dQ=w1358-h1022-s-no-gm?authuser=0)

## The part I didn't know I needed

Before connecting the battery, I reread the controller manual. It says you need a precharge resistor before you ever power it up.

The controller has big capacitors on its input. Empty capacitors look like a short circuit for a split second. Close a contactor and slam 120-plus volts onto them, and the surge of current can damage the controller.

A precharge resistor sits across the main contactor and lets current trickle in first. The capacitors fill slowly. When the contactor closes, there's almost nothing left to surge.

My design didn't have one. It wasn't on the parts list or the wiring diagram. I'd much rather find that out reading a manual than by smelling it. Replacing the controller would have cost about $700 and another long wait for shipping from China.

I spent some time wondering whether the resistor needed its own contactor to switch it in and out. It doesn't. Kelly's reference design wires a 2,000-ohm, 20-watt resistor permanently across the main contactor. At my pack voltage that works out to about 65 milliamps and 8.5 watts, well inside its rating. Once the main contactor closes, the resistor is bypassed and stops mattering.

Finding one that matched those exact specs took a long time. I ended up getting it from Mouser Electronics.

![the precharge resistor](https://lh3.googleusercontent.com/pw/AP1GczMWxSjKzMJeLL04JxkwMdtdpJ6VNnahHPBAfBlC9zItyk8rzPfxLAegZ9NtOVVuZcVRDroexu8_Vwp8kbNxLiHHID6rXTDsw2Zv--6gS-UT4wezKtlkAww8LVDuOU_1gfrvMuIs93tA9XzDRilRL8Z3kw=w1358-h1022-s-no-gm?authuser=0)

## The part I decided I didn't need

The same manual shows a reversing contactor in its wiring diagram. It flips the polarity to the motor so it spins backward.

At first I assumed the controller handled reversing internally. It has a "reverse" input pin, so why wouldn't it? That assumption is why I went as far down the electrical reversing route as I did. The pin only tells the controller the car is in reverse. Something else still has to flip the motor.

I went looking for one rated for my pack. The single-part options from Kelly and Albright advertise high coil voltages, but the contacts themselves are rated well under my 120 to 130 volts. The parts that could handle it meant building my own reversing circuit from two contactors and an interlock. More parts. More ways to fail.

Then I remembered I have a transmission. The Bug still has its stock four-speed, reverse gear included. There's no clutch, so every shift happens from a dead stop with the motor not turning. Putting it in reverse works exactly like it did when this car burned gas.

So no reversing contactor. The stock reverse-light switch on the transmission now tells the controller when the car is in reverse, and the controller drives a backup buzzer. That switch is there because of a federal backup-light rule from the '70s. Fifty years later it has a new job.

## Wiring it all up

With both questions answered, I finished the bench wiring: brake switch, reverse switch, main contactor, pedal, motor temperature sensor and the new precharge resistor.

![the fully wired bench](https://lh3.googleusercontent.com/pw/AP1GczOC0Y73r889G0ZsTFd-otFgRBWh3Rm5zegMjJqwBCQVOHp9z-FXyN33GFdK3E4gwJGbyQ3M7n11kQ8JnL2eePBUlh5Gy13oXdoJLrKF6vvzgNyT5h4Lb9tV_PtkRZpwrlRQELtEuMCBlakTn-fa2ibsLg=w1358-h1022-s-no-gm?authuser=0)

Then I connected the battery.

## First spin

I didn't touch the pedal right away. First I checked voltages across the contactor and at several other points. The precharge did its job.

Then I tested every other switch before the accelerator: emergency off, brake and reverse. For each one I watched the current draw on the 12-volt supply and watched the controller for error codes. Nothing complained.

Last came the accelerator. I pressed it very gently, and the motor turned.

I kept it to small nudges. The WarP9 is a series-wound DC motor. With nothing attached to the shaft, nothing holds its speed back, and it will climb RPM fast. That's hard on the brushes and risks overspinning the motor. Real throttle waits until it's bolted to the transmission.

![first spin](https://lh3.googleusercontent.com/pw/AP1GczPvIe57p35bO3CfakXdAUJiIyk_EjDqjkWf0lhwjeX5yVg8EfFGjQRliy1XORxfAuKeJgWLe9wAfQMVgMZLWRvTspmJ_I4kGFLor1zEFYCvyBOtTgTFilSOg2NyKfGtm2uIuw9w1hyi7Va_PvQLDd430w=w982-h1304-s-no-gm?authuser=0)

## One more safety gap

The precharge resistor has a side effect. The controller is never fully dead just because the main contactor opens. A little voltage always leaks past through the resistor.

That made me realize nothing on this car is a true off switch. When my hands are inside it, I want a physical plug I can pull out and put in my pocket. That part is called a manual service disconnect. Finding a trustworthy one has turned into its own search, and it's still open. It doesn't block bench testing, but it does block the battery going into the car.

## What's next

The bench isn't done yet. The charging system and the converter that turns high voltage into 12 volts both still need to go on the bench. I think the charging system is next.

In the meantime I'm still hunting for a service disconnect. The motor also still needs to be coupled to the transmission, which runs through the machinist I found back in May. No news there yet.

[All the VW EV Conversion posts](/vw-ev-conversion)
