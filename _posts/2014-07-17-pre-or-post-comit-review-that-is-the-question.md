---
layout: post
title: "Pre or post commit review: that is the question"
description: "Comparison of pre and post commit review"
category: programming
tags: [code review]
---
{% include JB/setup %}
I have an opportunity to work with all code review styles - No, Pre and Post commit. In this post I'm going to show the differences and compare the strong and weak side of every style.

###Code review makes a difference.

If you don't do code review you should start now. No matter on what project you are working, even if you are an indie developer or a freelancer, a second pair of eyes are necessary in our occupation. It's not about "good practices" it is about professionalism. Simply to keep the code maintainable we need to ask somebody if they understand it.

Another aspect of code review is that it allows us to detect the wrong use of framework or bad structures early before it propagates to rest of the system. I've a chance to work with a guy who has a strong background in Java. Unfortunately we write in C# and we put him on a new project which was apart of bigger e-commerce platform. It looks common, the new guy was employed, he has never used our technology stack but he quickly learned how to write to satisfy the compiler and customer. But after a while I needed to fix a small part of his job, and when I opened the document I saw an invalid use of C#'s extension method. Instead of `str.ExtensionMethod()` everywhere in code was `ExtensionClass.ExtensionMethod(str).` The compiler was happy with this and it works as the customer wanted but not what we (the developers) wanted to read. Finally, this was lowest level bug that I found there, this guy didn't learn from his errors. I'm no longer working there and neither is he.

###It is not the process it's the culture.

I hope this little story will convince you that code review is a must if we care about our product. I heard once that a scrum team member didn't want do a code review and he said that code review is a process that doesn't fit in with Agile techniques. For me he, I think he was afraid of sharing his code with other folks and what's more important he could be afraid of critique about his work. It's really hard to work with these kinds of persons and if you do, maybe you should stop and move on, because every time someone makes a pull request they should be ready to hear comments, not only criticisms, but also approvals of what a good job that they did. "Be proud of your code" should be our motto and code review will help us make our own code even better.

Another thing that pushed me towards code review is sharing knowledge. I don't need to have meetings with my folks if I know what they developed. I just read their code and know on which part of the system they are working.

Let's go back to the subject and start with pre commit review. I've used Code Brag for it within 3 developer project for 3 months. I must admit CodeBrag is great tool for this it allows you to not only comment lines, files or whole commit but also to like it like. And that feature is missing in other code review tools but is  useful.

###Pros of post commit code review

Time... post commit code review give your team chance to work whenever they wont because it won't stop any of you with developing new functionality. Second thing I found  important is noise reduction comparing to pre commit review where you need to stop your normal work (jump of the zone) review some code and get back. Task shifting is killing us. Usually I did code review at beginning, middle (before of after lunch) and at the end of work. 

### So what's wrong with it?

You cannot force others to apply suggested changes. Maybe the force is wrong word here but I hope you get my point. Because suggestion done in code review are not specific tasks I manage them for myself on Trello. I review comments and put them on board and fix them when I have some spare time only really critical bugs that were found were fixed immediately, but this happens once or twice. 

Since we do post commit review we review only commits on master branch and this means sometimes build failed. Orthodox git users will claim that this should never happened but workaround for this is release branch that is updated once a week with fully working version that could be deployed.

### Moving to pre commit review

After time I used no review and post commit review I settle in company that use post commit review. We use Stash. What's great with it is my code is approved by at least 2 people and has been checked by CI system so I am perfectly sure that it's working and it's supposed and what's more valuable it's clear for others. 

>"Working but unclear code is worst than not working but clean code because second one could be quickly fixed while first one can't be touched"

### Reality is not so great

When end of sprint come and everybody commits their changes in rush it's hard to code and review. It's not a problem if you have many people to review but there are days when half of the team is on meeting with important client, somebody take day off and you need to merge your changes to fix some nasty bugs that appear only on test environment because of network communication latency. There is no silver bullet for it. Maybe we should never allow this situation to happen.

### What code review style should be used?

As always it depends. If you work with small team (less than 5 I guess) or your team is distributed around the world, definitely use post commit review. It's lightweight and could be easily tuned to your needs.

If you work with bigger team and you work in one office (and probably in one room) and you meet at coffee break and could discuss about code pre commit is for you.

**Final conclusion is ["JUST DO IT!"](http://blog.codinghorror.com/code-reviews-just-do-it/)**
