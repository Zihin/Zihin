---
layout:     post
title:      "The Dining Philosophers Problem"
tags:       [Operation System, Story]
categories: [Operation System]
---

The dining philosophers problem is a classic concurrency problem dealing with synchronization. Gather round and I'll tell you how it goes:

![](http://upload-images.jianshu.io/upload_images/1218580-024da0df8d3a2a53.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Five philosophers are sitting at a table.


Now, each philosopher has two forks: left fork and right fork. If a Swanson gets two forks, he can eat! 

![](http://upload-images.jianshu.io/upload_images/1218580-fabdc78cc3ec700f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

If he only has one fork he can't eat :( 


![](http://upload-images.jianshu.io/upload_images/1218580-a0769cdd0b21abef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

So the Swansons need to learn to share forks: 

![](http://upload-images.jianshu.io/upload_images/1218580-8c254f48a1d2d11a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

The dining philosophers problem is: **how do you make sure every Swanson gets to eat?**


# Deadlock
Don't get me wrong, I love Swansons. But damn they are competitive. As soon as I told them to start eating, every Swanson grabbed a fork:

![](http://upload-images.jianshu.io/upload_images/1218580-1ef33bdb152d0b40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


And then they waited for someone to give up their fork so they could eat. But of course, "a Swanson never gives up his fork!" sigh So they waited forever and eventually died in their stupid log cabin. Great job, guys. When all Swansons are stuck, that is called ***deadlock***.

# Livelock
Alright Rons. I'm going to set a time limit. If you have been waiting for a fork for 10 minutes, you need to give up your fork. And wait 10 minutes before you try to pick up a fork again. By then, someone else will be done and you can use his fork:

![](http://upload-images.jianshu.io/upload_images/1218580-e0924509605ec4b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Now you can't have deadlock. But if all Swansons do these actions at the exact same time, you now have livelock:
Yay! Nothing can go wrong now! Right?
30 minutes later
So let me get this straight...
1. You all picked up your fork at the exact same time.
2. 10 minutes later, you all put down your forks.
3. 10 minutes later, you just picked up your forks again! [This will go on forever](https://en.wikipedia.org/wiki/Deadlock#Livelock)!
 
![](http://upload-images.jianshu.io/upload_images/1218580-00258cf8f57753a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


What do, nephew? You Swansons will [starve](https://en.wikipedia.org/wiki/Starvation_(computer_science))!
# Resource Hierarchy
Let's number the forks:

![](http://upload-images.jianshu.io/upload_images/1218580-19e312112693e096.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Now Rons, the rule is, if you're using two forks, you need to pick up the lower numbered fork first.
Now let's see what happens:

![](http://upload-images.jianshu.io/upload_images/1218580-62d3ee091d7e94a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


- Ron #1 picks up fork #1
- Ron #2 picks up fork #2
- Ron #3 picks up fork #3
- Ron #4 picks up fork #4
- Ron #5 can't pick up fork #5! Because he will need two forks and he needs to pick up the lower numbered fork first!

So fork #5 goes to Ron #4 – no deadlock!

![](http://upload-images.jianshu.io/upload_images/1218580-810ef2db27079485.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Cool, resource hierarchy avoids deadlocks! But it is slow. Suppose you have forks #3 and #5. Then you decide you need fork #2. Well forks #3 and #5 are larger numbers. So you'll have to:
1. put down fork #5
2. put down fork #3 (the order you put these down in doesn't matter)
3. pick up fork #2
4. pick up fork #3
5. pick up fork #5

Ugh, what a waste of time!

# Semaphores
Here's an easier solution: if there are 5 forks, only 4 Swansons should be allowed at the table. We'll have a waiter control access to the table:

![](http://upload-images.jianshu.io/upload_images/1218580-31ab49e3cc51b386.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



If there are < 4 Swansons on the table, you can join. Otherwise you have to wait until there are < 4 Swansons!
Ok, this prevents deadlock, but you can still have starvation...a Swanson could wait forever and never get to sit at the table. Unless he kills off one of the other Swansons.

# Chandy/Misra
Now I've got it. All forks can be clean or dirty: 
![](http://upload-images.jianshu.io/upload_images/1218580-6ec56a2ebfca76e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Initially all forks are dirty: 


![](http://upload-images.jianshu.io/upload_images/1218580-ba90d9469324915c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Now:
1. Number all the Swansons 
![](http://upload-images.jianshu.io/upload_images/1218580-bc1639412b7ecca6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2. For every pair of Swansons, give the fork to the guy with the smaller id:
![](http://upload-images.jianshu.io/upload_images/1218580-ab916d05d77c37c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. When a Swanson needs a fork, he asks his neighbor for his fork. When his neighbor gets the request:
  - if his fork is clean, he keeps it.
  - if his fork is dirty, he cleans it and sends it over.

When a Swanson has eaten, all his forks become dirty.
Bam! Starvation problem solved! The guys who are starving get a higher priority than the guys who are eating!


**Q.** Swansons 3 and 4 both only have one fork. Suppose Swanson #3 requests a second fork from Swanson #4. Will Swanson #4 give up his fork even though he didn't eat?
**A.** YES. According to the rules of Chandy-Misra, Swanson #4 would have to clean his fork and send it over to Swanson #3.
