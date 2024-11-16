---
layout: page
title:  "Maintaining CTF Skills With Spaced Repetition"
date:   2024-11-15 19:24:51 -0500
categories: anki security
---

I'm a longtime player of [security ctfs][wiki-ctf].
However, as I've gotten older, I've had less time to play.
When I do play, I've often been frustrated when I have difficulty with problems that I was able to solve years earlier.
My underlying knowledge is there, but so is a good amount of rust.

## Spaced Repetition
A good friend told me about how he and his med school classmates all heavily use [spaced repetition][spaced-rep] to study.
In short, there's significant evidence that spreading out study of a topic over time drastically improves retention.
As you learn a topic, you increase the time between reviews of that topic.
If you ever do poorly during a review, the time between reviews decreases.

There are many existing systems that automate spaced repetitions, typically around flashcards.
The standard guidance is to make simple atomic facts, with the prototypical example being vocabulary practice.
One of the most popular implementations is [Anki][anki-homepage].

Here's an example of a math fact in my Anki deck.
I'm initially prompted with the top half of the image, before receiving the answer at the bottom.
Depending on how I feel I answered, I then decide when I should see the question again.
Anki manages which cards I see each day, and calculates the recommended delay between reviews.

![Anki Example](/assets/anki-example.png)

Before starting this project, I had been using Anki for eight months, mainly with a small selection of programming and cooking facts.

## Pwn College

[Pwn College][pwn-college] is a series of classes on computer security hosted free online by Arizona State University.
It consists of recorded lectures, with accompanying CTF style exercises in a Linux environment.
Each set of exercises starts simple, and increases in difficulty.

For example, their [web security][pwn-college-web] section starts with basic path traversals and command line injections, before progressing to SQL injection, XSS, and CSRF.
Later lessons progress from introductory memory corruption, to complex heap exploits and micro-architecture attacks, such as [Spectre][spectre].

I had previously completed the heap exploitation lessons over the 2020 holidays.
However, since I only do a handful of CTFs per year, I had mostly forgotten this topic when I tried to solve a problem during a CTF in summer 2023.

## Spaced Repetition Applied to Pwn College
Thus, I decided to combine the two, and use Anki to schedule review of Pwn College problems.
I'd start with a lesson, and solve many problems back to back.
Once I felt I sufficiently mastered it, I'd then add it to my Anki deck, to space out review over time.

### Approach:
- Start with lessons I'm comfortable doing, but could benefit from practice. I decided to start with shellcoding, and work through heap exploitation.
- Choose problems in each lesson of suitable difficulty. Make sure each tests the knowledge I want to know, but without being over niche.
- Have one Anki card per lesson, which randomly chooses a single problem for me to solve.
- Add only a few lessons per month, to avoid being crushed by reviews.
- When a lesson comes up for review, try to complete it during time for side projects. This generally meant a small window on weekends, avoiding holidays.
- A successful review is when I'm able to solve the problem in a reasonable amount of time, without overly depending on references.
    - I was fine with making mistakes, but wanted to be solve everything efficiently, and with good use of tools.

Here's and example card, using Anki addon to randomly select a problem.
![Anki Heap](/assets/anki-heap.png)

## Pitfalls
Along the way, I had several small, but important lessons learned.

First, I had to make sure I was choosing the right problems to review.
Many Pwn College exercises have .0 and .1 parts.
The .0 challenge contains debug support, such as printing heap addresses, or providing better timing control over a race condition.
The .1 challenge then is essentially the same challenge, with that support removed.
This ensures that you're not relying on the debug assistance as part of your exploit.
I personally found that the debug printing wasn't an issue, as long as I knew how I could get the same information in GDB.
However, I ran into issues with the race conditions problems, as the .1 challenges required timing techniques that the .0 problems did not.
Because of this, when adding a new Anki card for a lesson, I ahd to deliberately decide which exercises would be on the card.

Second, I found it important to balance when I did reviews, as getting behind on Anki cards can be discouraging.
Over the summer, I had several time consuming reviews get scheduled at the same time as work travel.
Coming back from the trip with several hours of "work" on this side project didn't feel great.
I got through it by knocking out one review per weekend until I was caught up.
If I happened to have had a higher density of reviews, I could have gotten bogged down and frustrated.
My key lesson learned here is that it's important to focus on the content I want to retain, while also feeling fine deleting an Anki card if I decide it's no longer worth the time. 

## Advantages over Standard Pwn College 
Along the way, I found one unexpected upside to this approach.
A number of Pwn College modules have earlier challenge provide exploitation primitives that later challenges then use.
For example, the [Exploitation Primitives][expl-prims] lesson requires using a multi-threaded race condition to build memory corruption primitives.
Initial challenges in the module require you to construct arbitrary alloc, arbitrary read and arbitrary write.  
Later challenges then use these primitives to bypass ASLR of multiple memory regions, and gain full remote code execution.

In my view, this lesson has two key parts: how to turn the race condition into stable primitives, and then how to use those primitives to get full execution.
A student working through this module normally only really has to write the primitives once, as they can be reused later.
However, my approach is to avoid using previous solutions in each review, and thus I've had more repetitions on these base primitives than in a traditional approach.

## Other Applications
Throughout this process, I've found several other projects using a similar spaced repetition approach with more complex material than facts that fit on a single flashcard.
Around the same time as starting this project, I also started [Math Academy][math-acad], a startup that provides online math classes that also uses spaced repetition.
I may write about them in a future post, and can't recommend them enough!

I've personally completed [Rustlings](rustlings), and added Anki cards for that as well. 
Similarly, there are a number of resources for spaced review of [Leetcode][google-leetcode] style problems, although I haven't personally tried them.

## Results

The big question: Does this approach make me a better CTFer, and reduce my frustration from a year ago?

I believe so, but it's difficult to quantify.

I'm definitely much better at Pwn College problems, and am more fluid with tools that I'd already been using for a while (Pwntools, Binary Ninja, GDB w/ plugins).

In the CTFs I've done of the last year, I've worked on cryptography, web, and V8 challenges, which have had less direct tie-ins to my Anki cards.
That said, I've definitely enjoyed this as a side project, and plan to apply this approach to similar topics in the future!

[wiki-ctf]: https://en.wikipedia.org/wiki/Capture_the_flag_(cybersecurity)
[spaced-rep]: https://en.wikipedia.org/wiki/Spaced_repetition
[anki-homepage]: https://apps.ankiweb.net/index.html
[pwn-college]: https://pwn.college/
[pwn-college-web]: https://pwn.college/intro-to-cybersecurity/web-security/
[spectre]: https://en.wikipedia.org/wiki/Spectre_(security_vulnerability)
[expl-prims]: https://pwn.college/software-exploitation/memory-mastery/
[math-acad]: https://www.mathacademy.com/how-it-works
[rustlings]: https://github.com/rust-lang/rustlings
[google-leetcode]: https://www.google.com/search?q=leetcode+spaced+repetition
