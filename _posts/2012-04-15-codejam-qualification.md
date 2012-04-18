---
layout: post
title: Code Jam 2012 – Qualification Round
---

I qualified for Google Code Jam 2012 yesterday.

I began in the afternoon, well into the round, because I didn't want to stay up
late—the start of qualification was 12am in Germany. Having solved only one
practice problem before on Friday I didn't exactly feel "limbered up" at that
point, but I had some basic Ruby stdin/stdout workflows memorized again.

Upon reading the problems again, I just realized how ridiculously simple
["Speaking in
Tongues"](http://code.google.com/codejam/contest/1460488/dashboard#s=p0)
must've really been (which is also what I was told on Google+ today) but back
then, I panicked—even without the requirement to do particularly well—and went
straight for the other problem descriptions.

I settled on ["Recycled
Numbers"](http://code.google.com/codejam/contest/1460488/dashboard#s=p2) as the
first one to tackle. Brain partly locking up (I guess) it took me a short while
to figure out actually how to traverse the possibilities to check for, which
then turned into a straightforward implementation that was done rather swiftly.

The authors' statement on them being "sure about the output to Case \#4" had me
hunting the last bug—my output being 288, one larger—for quite some time.
I realized that it had to be a duplicate pair of numbers somewhere, but at the
time it didn't really occur to me how this should happen, so I took the
*not-so-clever* approach—as in, I wouldn't want to ressort to that in an
interview with the stakes being high—of manually going through the outputs of
case \#4, until I stumbled upon 1212 generating both 2121 (in the form of
212|1) and, well, 2121 (in the form of 2|121). Which made a lot of sense. Silly
me.

I fixed that rather bluntly by keeping track of the pairs generated, with the
overhead of object creation probably contributing to less than amazing running
time of the algorithm, but I wanted to be done with it and alas: first small
input went through correctly in about two or three seconds.

Satisfaction I then promptly ruined with the large input. I fired it up, sat
back, figured it'd be running a little longer than three seconds—I only tried
one test case with the bounds being 1 and 2000000 before that, to get a sense
of the dimensions and whether my approach would be feasible at all, with using
Ruby etc.—and got the silly idea of `tail`'ing the output file to see progress
… of which there wasn't any. *At all.*

Now, I'm not too sure about what *should* have happened there—straightforward
suspicion being some buffering somewhere, as my test right now shows output
after 50 test cases but then hangs, even after the program has finished—but
after panicking and aborting the run two or three times (with maybe three
minutes left in the end) I realized that output was in fact being written. Just
not, you know, picked up by `tail`. So I started it up one last time aaaaand
THERE WENT THE DEADLINE.

*Really* disappointing.

Wall time now when trying it again says 2 minutes 49 seconds, with 2 minutes 46
seconds spent in userland crunching numbers. So it would've worked out, if
only. Oh well.

The last problem—enough points for the small input to qualify, which is where
I stopped (after getting the large input correctly as well), because I wasn't
feeling too frisky and wanted to do something else with the rest of the day—was
["Dancing With The
Googlers"](http://code.google.com/codejam/contest/1460488/dashboard#s=p1),
a nice, kind of real world one.

Start with the total scores sorted, divide each by three, decide whether they
can reach the minimum best score in any way and decrement the allowed
"surprising cases" whenever one occurs. Easy enough.

Except I made a stupid mistake. Plus another. And then some.

So it took me *seven* (!) incorrect small inputs until I finally got it right.
Lots of "fixing that small error over there" and not properly thinking the
whole thing through again. I'm not proud of that. Such performance in an
interview would likely have resulted in an epic fail. But then again, my mind
wasn't too fresh yesterday.

### Conclusion ###

I don't think I will stand any chance against the masses of lightning-fast
coders with their razor-sharp minds from all over the world (though especially
China and Russia seem to rule) to advance in one of the next rounds. I panic
way too easily when faced with a clock almost audibly ticking, something I've
just barely managed to keep in check in the phone screens leading up to my
internship at Google in London last year. (I'm still a bit puzzled I got in
back then and get to go back for another one this year, but they seemed to like
my work.)

But if anything, it will be a very good way of warming up to that pressure and
dealing with it, so I guess I'll just keep at it.

