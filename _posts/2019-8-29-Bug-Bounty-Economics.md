---
layout: post
title: Bug Bounty Economics
---

# Economics of bug bounty hunting
Hello! This is my first time presenting my thoughts about bug bounty to the public, so I'd like to start with a short self introduction.

## whoami
My name is Dmitriy and I'm have been a full-time bug-bounty hunter since 2016. I ran into Hackerone in the summer of 2015. It was during the time when things were not going very well with my Ad Tech start up. I was always interested in web security and looking for bugs surprisingly turned out to be a hobby, which can pay some bills. By the end of 2015 i left my start-up thinking that I'll take a break for a few months and then decide what I want to do next. In the following months my little bug hunting hobby went pretty well. I signed up on Bugcrowd and Synack. Then joined a $250k challenge organized by Mark Litchfield (thanks, Mark!) and realized that i can do this bug-hunting full time.

## Introduction
Bug-hunting is a great area, where you can be rewarded for solving hard intellectual challenges. The intellectual challenge part has always been (and i hope it will continue to be) a source of motivation for me. The fact that I was able to exploit a super tricky bug can be incredibly emotionally rewarding. In this article i want to speak about other side of the bug-bounty hunting — economical success.

Bug-hunting is a field that most of the time is individual work. Two obvious economical success metrics for an individual are earnings ($) and hourly rate (**$Rate = $/hr**).

Every experienced bug-hunter has a sense that helps him understand which programs are worth the attention and which ones are not worth spending the time.

So how do you tell which program is good? The key metric here is hourly rate, that you are making on a program. Of course, programs and platforms pay for bugs, not for the hours spent. Finding bugs is a stochastic process, so we can correctly measure $/hr only after spending a decent amount of time on a program. However, pretty fast you intuitively evaluate (more likely, compare to other programs) your expected $/hr value and make a decision regarding spending the time on the program.

## Hourly rate ($Rate)
Earnings are calculated in a obvious way:

 **Earnings = $Rate * Hours**

What affects your hourly rate **$Rate** as a bug hunter?
To keep things simple, these are 3 most important things:
1. Probability of finding a bug
2. Payout for the bug
3. Chances of being duped.

The formula here will be:

**$Rate = SUM ( ProbabilityOfFindingBug \* Payout \* (1 - DupeChance))**

**SUM** here represents a sum across all bug classes, that you are looking into.

Every full-time bug-hunter dreams to be as good as [@thedawgyg](https://twitter.com/thedawgyg "@thedawgyg") with his [$29k/hr](https://www.zdnet.com/article/relying-on-bug-bounties-not-appropriate-risk-management-katie-moussouris/ "$29k/hr") :). So to be successful (in economical terms) you need to maximize your $/hr rate.

## Maximizing $Rate

After we know the formula it's easy to understand what to do:
1. Look for programs / places / bug classes which have the biggest bug expected value (**Bug$EV = ProbabilityOfFindingBug \* Payout**)
2. Minimize the chances of being duped.

#### Finding bugs with the biggest expected value (Bug$EV)

Bug Expected Value is **ProbabilityOfFindingBug * Payout**.

Ideally, you want to hunt on a decent paying program, where you have a high probability of finding a bug. It is worth noting that your chances of finding a bug in the best paying programs are usually pretty low. So if you choose to go for hard targets, your income variance will be high — in July you might get $5k, in August you might get $50k, in September you might get $0 :)

So if you prefer steady income, it might worth it to look for lower paying programs/bugs, which have higher chances of vulnerability discovery.

This trivial bug EV formula might also lead to some interesting particularities.

Imagine, that you get invited into program with a big scope. 
Program payment table says:
- Reflected XSS - $250
- Stored XSS — $1000
- RCE — $2000

What should you focus on? I think it should be on Stored XSS. The probability of finding it is usually much higher than the chances of finding RCE. The probability of finding Reflected XSS should be the highest, but the reward for it is 4 times less.  On top of that you'll have the highest chances of being duped.

As an example, on the Verizon Media program, looking at their bounty table I believe that this is exactly the case for them and SSRF/XXE.

#### Decreasing the chances of being duped
For usual programs, everything is pretty straightforward:
1. Look at parts of scope with less competition (things that are harder to set up, areas that require you to buy subscription and etc)
2. Look at programs with less competition
3. Focus on bug classes with less competition (CSRF usually has a much higher chance of being a duplicate than RCE)

Things can also change dramatically if you have access to the list of submitted bugs (i.e. Analytics in Synack). This can significantly decrease your chances of being duped.

I remember doing calculations after my first year in bug bounty and it turned out that on H1 i had around 30% duplicate reports and on Synack it was less than 10%.

## Other things to take into account

To keep things simple, we talked about only 3 parameters: Probability of finding a bug, Payout for the bug, and the Chances of being duped.
But there are more things, that can be taken into account:
1. Chances of getting N/A / OOS(out of scope)
If you report something that is not clearly in scope, then you might be simply wasting your time.
2. Chances of being paid
There's always a chance that a program will ignore your report, shut down or refuse to pay for other reasons.
3. Chances of being invited to a event/program
You may receive invites to programs and live events based on your previous activity. Sometimes it might mean that to receive a juicy invite you need to spend time on a program, which is not the best in terms of **$Rate**.

For \#3 I have a good example of this where i fell victim to my own attitude. I was invited to two previous H1-702 events. Each time I spent some time looking for bugs, but the targets were not looking very promising in terms of $/hr for me. As a result I did not perform well enough to be invited this year. And guess what? This year they had biggest event of all time :)


## Switching between programs or sticking to the best one?

Sometimes you get into situations where you keep exploring one program and stick to it for months. It is paying well, but you keep receiving new invites. The main issue here is that it's hard to evaluate a new program without testing it and submitting at least one report.

Fortunately, this situation is known in math as [Multi-armed bandit problem](https://en.wikipedia.org/wiki/Multi-armed_bandit "Multi-armed bandit problem"). It turns out, that leaving 10% of your time to explore and evaluate new targets is a good way to maximize your earnings.
