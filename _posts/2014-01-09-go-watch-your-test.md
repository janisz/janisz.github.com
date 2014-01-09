---
layout: post
title: "Go watch your test"
description: "Short example how to use Watch with go code"
category: programming
tags: [go, tdd]
---
{% include JB/setup %}

In TDD we tend to write test before we write code. And then try to write code that pass our tests. This is one of
the most productive (in long term) way of developing applications. How we can make it even more productive?

Look at your routine. You write test. Compile it and run. Fix if it's not compiling then you write code. Compile program
run tests and write new test. Here are two steps that may be kicked off. In modern programing languages compilation can be
done on the fly. Moreover modern machines can handle multitasking so why on the hell we don't run our tests in background?

I found great tool called [Watch](https://github.com/eaburns/Watch). Name is meaningful and if you think about GNU/Linux
tool called `watch` you are one a good way.
Watch is a tool that runs specific command but instead of firing periodically like `watch`, it monitors current
working directory and run command when something change.

Because `go` programs compiles really [quick](http://stackoverflow.com/q/2976630/1387612) it is possible to see result
of compilation without even noticing that it was done. Another thing if you have tests you can run them all while you are
coding and see your progress without asking your IDE to do it for you. Below I will show how it works for me.

To run all test for my project I use following command. Don't be afraid of using it. I use `awk` to make output from tests
more readable and easier to detect errors.

	Watch -t go test ./... | awk '/?/ {print "\033[33m" $0 "\033[39m"; next}
		/ok/ {print "\033[32m" $0 "\033[39m"; next}
		/FAIL/ {print "\033[31m" $0 "\033[39m"; next }
		1 {print}'

And how it looks in practice (I was editing source on another screen)

<iframe src="http://showterm.io/c2e02792be7389b2e010d" width="100%" height="200" align="middle"></iframe>