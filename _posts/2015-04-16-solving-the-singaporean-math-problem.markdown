---
layout: post
title: "Solving the Singaporean Math Problem"
date: 2015-04-16 09:04:38 -0700
comments: true
categories: fun, learning, solving
---

Trending today seems to be problem number 24 of a [Singaporean Math Olympiad test](http://www.cnn.com/2015/04/15/living/feat-cheryl-birthday-math-problem-goes-viral/). Let's not get bogged down why suddenly the Internet is clamouring over solving a seemingly impossible math problem, but since everyone wants to figure out the answer, let's go through how to get it.

Disclaimer: I have not consulted any outside sources to verify my answer, but I'm fairly certain my logic is sound.

<!-- more -->

## The problem

The problem is straightforward. Albert and Bernard just met a girl named Cheryl. They want to know her birthday. Unfortunately, Cheryl is either a troll or is just a troubled soul (tr-oul?) and decides to make them earn that knowledge.

She gives them a list of possibilities of when her birthday will be:

- May 15
- May 16
- May 19
- June 17
- June 18
- July 14
- July 16
- August 14
- August 15
- August 17

Then, since that clearly isn't enough, she tells Albert the month of her birthday, and she tells Bernard the day of her birthday. 

At this point, any normal human being would have just told the other dude what Cheryl told them, but not Albert and Bernard! 

They conversed briefly:

```
Albert: I don't know when Cheryl's birthday is, but I know that Bernard does not know too [sic].
Bernard: At first I don't [sic] know when Cheryl's birthday is, but I know now.
Albert: Then I also know when Cheryl's birthday is.
```

Okay, is that confusing enough for you? 

Let's break the problem down. 

## The solution

The key is not to solve the problem yourself, but to look at it from the lenses of Albert and Bernard. 

Let's look at the conversation between Albert and Bernard. Albert is given X month, Bernard is given Y day.

Since Albert only knows the month, any month with more than one date listed is an uncertainty. This part was obvious. What isn't obvious is the implication of Albert knowing that Bernard does not know when Cheryl's birthday is. 

```
Albert: I don't know when Cheryl's birthday is, but I know that Bernard does not know too [sic].
```

How could Albert know for sure that Bernard doesn't know, despite not knowing what Bernard knows?

The answer is that ALL the listed dates within Albert's month MUST be duplicates. 

Why? Well, let's say Bernard had the 18th. Right at the onset, Bernard would know the month, since there is only one month with the 18th (June). Same with the 19th. So we know that Bernard got neither the 18th nor the 19th. 

Now, Albert KNOWS that Bernard does not know when her birthday is. By extension, this means that Albert knows that Bernard got a number that was a duplicate. 

How can Albert know for sure that Bernard's number was a duplicate? Because all of the numbers in Albert's month were duplicates. 

This means we can safely rule out May and June, as both of those months have a singleton date (19 and 18 respectively).

So by the first statement, we've ruled out May and June, and are left with the following...

- July 14
- July 16
- August 14
- August 15
- August 17

Okay, let's analyze Bernard's statement.

``` 
Bernard: At first I don't [sic] know when Cheryl's birthday is, but I know now.
```

Let's say, for argument's sake, that Bernard was given 14. Would he be able to discern the month? The answer is no, since July and August both have 14. This means that Bernard's number must be 15, 16, or 17. 

Now, if he got 15 or 17, then he knows the month must be August. If he got 16, he knows the month must be July.

So, simply by Albert saying that he knows Bernard doesn't know Cheryl's birthday, Bernard's number makes it obvious to Bernard what the birthday is. We still don't know, however. _And neither does Albert_, which is a key point I'll come to in a second.

So we've ruled out July 14 and August 14. Let's keep going.

- July 16
- August 15
- August 17

Finally, the last statement, and the answer you've been waiting for. 

```
Albert: Then I also know when Cheryl's birthday is.
```

Remember, Albert knows the month, but not the day. If Albert now knows Cheryl's birthday, we can safely rule out August because he still wouldn't have enough information (since there's 15 and 17). 

Therefore, the final answer is...

# July 16

Hope you had fun. Feel free to reach out at rasheed.bustamam@gmail.com if you have any questions or need any clarifications. 









