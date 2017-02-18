---
layout: post
title: Git Bash Shortcuts
---

### Background

I’ve been working in a software shop that uses Mac machines for all our dev machines for about 3 months now. Prior to this, I had some experience with the Unix environment, but had never done anything with bash scripts to make my life easier. I had absolutely no idea what I was missing.

### Slow Start

Less than two weeks into the job, I realized that typing out full branch names to checkout a branch was absolutely terrible and went through the process of setting up [git-completion.bash](http://code-worrier.com/blog/autocomplete-git/), which I found extremely helpful, but that was the extent of my quality of life improvements for a while.

About a month later, I realized I could alias commands in  `~/.bash_profile`. I’m more than a little ashamed of the fact that it took me so long to set up anything to help myself out, but I was finally getting it. I quickly set up a command to use psql and connect to our database.

### The Good Stuff

Today, I finally went through the process of making my life a lot easier. I set up lots of basic shortcuts to make git commands quicker and speed up things I was doing all day anyway. Then I finally realized I could do a lot better for myself.  One of the functions I set up was a shorthand for doing checkouts.

{% highlight bash %}

function co() {
	git checkout $1;
}

{% endhighlight %}

This could be used to checkout branches quickly with `co <branch_name>`. I also set up the functions `nb` and `db` that used a similar structure to create and delete branches.

I then realized that my solution could do more. Git branch tab auto-completion is great, but what if I could do better? Our branches at work all have their JIRA ticket number in the name, followed by a description. I decided to make a function to search on a string provided and checkout the matching branch.

{% highlight bash %}

function cbb() {
	branch=`git branch —list *$1*;`
	git checkout $branch;
}

{% endhighlight %}

I used the shorthand cbb for 'checkout bug branch', but really the shorthand doesn’t matter. You can make it anything short that's easy to remember.

My intended use for this was to use the JIRA ticket number with the checkout function, but it can be applied to any matching string. For example, I would have a branch name `web_9999_test_branch` for example. To check it out with our new script, we just need to run `cbb 9999` and our branch will be checked out.

### Next Steps

There’s also room for some improvement here on the string matching for multiple matches and allowing the user to select one and potentially prompting the user for a new branch name if no result is found, but I’ll leave that for another post.