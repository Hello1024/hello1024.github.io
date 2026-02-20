---
layout: post
title: AI is a winner-takes-all game.
---


Various people have talked about the lack of a 'moat' for AI companies, and so far that appears to be the case.    Lots of companies are producing LLM's and running them with razor thin margins, and all users flock from one service to another as better quality models are released.



But I believe that is going to come to an end soon.   A winner will emerge.   And here is why:

### On free plans, AI companies collect all input and output.

Up till now, there has been no good way to turn conversation histories from millions of users into improved AI models.    Yes, there are a few approaches for reinforcement learning from user 'happyness' signals, but not many - and each click of 'thumbs up' is a single 'bit' of data in a world where we want gigabytes.   It doesn't scale.

### Training from the 'final solution'
That is changing.    Agent models who try to achieve some task often try multiple solutions, and one succeeds.    That is a great training signal - the next version of the model can go straight to the perfect solution.    The more people use a particular companies LLM, the more examples of wrong and correct solutions will be found, and therefore the better it will get.


### Training from your private data
Thats only the start too.  Agent models often get to see a lot of content in the course of their work - code, webpages, etc.   All that data can be used for AI training too - and there is a lot more private code and text in the world than public code.    As well as being used for the pretraining, this data can be used for synthetic tasks.  Eg. "Take this users iOS app and imagine porting it to MS DOS".  "Take this users wedding speech and make it a rhyming poem without the letter 'e'".  "Take this set of company accounts and highlight potential illegal expenses".

They are mostly pointless tasks, but they're things where the result can be evaluated by another LLM, and that used to finetune the model.   Children do the same - building a tower of play blocks isn't a useful task, but it is good for learning.   Getting ahold of large amounts of user data is key to this approach.    Then you use an LLM to set the tasks, an LLM to evaluate the results, and then do differential training to reinforce more successful approaches to solving the problem.


### As compute gets cheaper, data will become the limiting factor

When data is the limiting factor, he who has more data gets better results.    And when you have better results, you get more users.  Those users give you more data, and the flywheel means that before long there will only be 1 leading AI company.    It will be the one who manages to extract most from user chat histories.
