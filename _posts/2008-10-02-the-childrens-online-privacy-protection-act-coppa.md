---
layout: post
title: The Children's Online Privacy Protection Act (COPPA)
permalink: coppa
tags: homeworq
---

A user asked me today, "Wouldn't it be nice if you could send an email when someone has an <a href="http://homeworq.com">overdue homework assignment</a>?"

The short answer:  I can't.

The long answer is the story of one among many trade-offs involved in creating a web site like HomeworQ.com.  And like many deep pits of anguish, despair, and regulation, this story begins with Congress.

## COPPA

In 1998, Congress passed the <a href="http://en.wikipedia.org/wiki/Children%27s_Online_Privacy_Protection_Act">Children's Online Privacy Protection Act</a>, or COPPA, trying to protect children from all the bad things that can happen on the internet.  This law is the reason you see all those "I am at least 13 years old" check boxes on web sites.  Even though 89% of twelve-year-olds, when confronted with "Sorry!  You must be at least 13" will just put their birth date as "1949".  I just made up that statistic, but you know it's true.

Nevertheless, COPPA is serious business, and there have been some <a href="http://www.msnbc.msn.com/id/14718350/">huge</a> <a href="http://www.ftc.gov/opa/2004/02/bonziumg.shtm">fines</a> when companies violated it.  I don't want to be one of them.

In short, COPPA says that if you can tell who a person is, through some kind of identifying information, and they are under 13 years old, then you must have parental permission to let them on your site.  I'm way over-simplifying (this is a law, after all - you know, by Congress), but that's the gist of it.

Now think for a second about just how hard it is to get parental permission for use of a web site.  Fortunately, taking a credit card counts, under the theory that most pre-teens don't have one, and that's what most sites do.  Also popular:  "You must be at least 13" messages, keeping at least the easily deterred pre-teens off your web site.

## HomeworQ.com

Our site is free to use, so the credit card option isn't very practical.  And although HomeworQ.com is really designed for high school and college students, we don't want to prevent anyone from using it, even middle and elementary school students.  So we know there are children on our site.

I really don't want to have to deal with the headache of notifying parents.

For me, it seems the best solution is just not to collect any personally identifying information.  That avoids the entire problem.

The only thing I really wanted to collect was email, which I wanted for two immediate requirements:  integration with <a href="http://en.gravatar.com/">Gravatar,</a> and password reset functionality.  There were other ways I could use someone's email address, but I could forsake those to free myself from COPPA if I could find some way to solve my immediate needs.

## The Technical Part

Fortunately, the Gravatar API doesn't use the email address, it uses a cryptographic hash of the email address.  If I just stored the hash, I could throw away the email address and integrate with Gravatar just fine.  Since the hash can't be easily converted back into an email address, it's not identifying information.  COPPA allows me to ask for an email, use it briefly, and throw it away without ever storing it in my database.  First problem solved!

The second problem involves what to do if a user forgets his password.  In this situation, many sites send an email with a reset link to the address the user provided when registering.  If only that user has access to that email inbox, then a bad guy can't impersonate you, change your password, and deny you access to your account.

I wanted to do something similar, but without the email address.  So when the user clicks the "forgot password" link, I ask him for his email, hash it, and compare the hash to the one stored in my database.  If they match, I know he's giving me the correct email address, I use it to send an email with the reset link, and then like before I throw away the email without ever storing it in the database.  Problem two solved!  (Conceptually, anyway - I'm still implementing this.  Don't forget your password yet.)

## So Here We Are

Without a doubt, email addresses are valuable.  I'd like to have them.  There are some nice features I could offer if only I had email, not to mention multitudes of vague possibilities that are surely out there if only I could imagine them.  But right now, I just want zero friction for new users.
