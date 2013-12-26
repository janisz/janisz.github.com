---
layout: post
title: "Merging style for post commit code review"
description: "IMO best way to merge for post commit code review"
category: git
tags: [git, merge, gitkata]
---
{% include JB/setup %}

Here is description of nice merging convention that I learned on [gitkata](http://v2.gitkata.pl/).

How you tree look like? Do you care how you merge? If you haven't ever look at your commits history then you
should do it now. I can recommend setting up alias like this

	 lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)' --abbrev-commit

What you can see. Can you tell what had happed with your code over the time using only git or you must take a look at
Redmine? If you see similar image to one below you definitely have a problem (even if you like rainbows).


<img style="float: left; margin: 10px;" src="/assets/images/messy_repo.png" alt="FileZilla logo">

Even if you see less drastic image of your your still it's not good.

<img style="float: left; margin: 10px;" src="/assets/images/cleaner_repo.png" alt="FileZilla logo">

For some time I'd believed that merge with commit is best option for maintaining code. I was totally convinced that this is
the best option. I start have doubts when one of my friends told me that his company enforce staight history.
I told him that he should swich to SVN but after time I must admit I was wrong.
Merge with commit is great. In any time you can say where you merged and who introduce bug. On the other hand it
adds unnecessary noise to source history. If we add commit whenever we pull code we will end with 10 branches and
nobody can tell what is going on. For detecting bug introduction we can use `git bisect` and even automate whole process.

How to prevent it? **Always pull with rebase**. Pretty simple but it will keep history linear and it will generate same
troubles with merging as normal pull. How to enforce it on all your coworkers. Agree with them on one common `.gitconfig`
it will solve problem. Another advantage of these approach is when you do a code review with merge commit your coworker
will see changes that was previously reviewed. There is no reason to add them work especially if they did it once.

That was easy. What we should do when somebody branched on feature branch and he want to merge his changes back? It
is a little bit complicated. This time I'll rather use commit merge instead of rebasing whole branch on the top o develop.
Then it will be totally clear when specified feature was done and what was changed. Another option is merging with squashed
commits but in my opinion we loose too much, nobody (even author) will know how he solve specified problem. If company
enforce TDD it's simple to check if he really start from tests if whole branch was squashed into one commit it's impossible.

Another reason why I'm against merging feature branch with fast forward is that when we do code review nobody is really
interested how we refactored our code before pushing it to server. People want to see changes between final product
and last commit from server. So the default approach is unacceptable because when we merge back and there was some work
done on develop branch it won't be totally clear what files was really was done for that feature when there will be more
branches merged over time.

I'll show what I'm talking about in simple example. Let's assume that we branch on feature branch and make our work while
somebody commit on master branch. On left is normal merging while right side shows merging with rebase


<img style="margin: 10px;" src="/assets/images/default_merging.png" alt="FileZilla logo">
<img style="margin: 10px;" src="/assets/images/rebase_merging.png" alt="FileZilla logo">


OK, this is silly example but when there will be more branches we will end with similar image as from first example. When
we rebase our feature branch onto branch that we want to merge with it will be totally clear what we did. Of course this
trick we can do only if we haven't pushed our feature branch in other case people who already pulled our code
will suffer from our rewriting history.

So what I did was quite easy. Instead of merging my feature branch just after pulling code, I rebase it onto desired branch
and then merge it with `--no-ff` option to force merge with commit.

In conclusion: There is nor magic rule how to merge. We always must think about our coworkers and have big picture
of what we do and every time decide how we should merge.