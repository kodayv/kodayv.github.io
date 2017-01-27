---
layout: essay
type: essay
title: ‘There is no such thing as a stupid question’ – Debunked!
date: 2017-01-26
labels:
  - forums
  - StackOverflow 
---

<img class="ui medium left floating image" src="../images/questions.jpg">

## Why smart questions are important for smart software engineers

The online world of software engineer’s forums is a place of shared knowledge for those who seek to tread through its many pages. When directing a question to the forum it is important to understand the audience that will be reading and answering your questions. These people are not your besties, nor can they read your mind. The questions asked need to be precise, directed, and with a demonstrated knowledge of what you are doing. 

## Smart question = Smart answer

First is an example of a smart question. The question title was called “Do a “git export” (like “svn export”)” with the tags ‘git’, ‘export’,  ‘git-archive’, and ‘svn-export’. Already the reader has a pretty good idea of what the questioner wants. If the reader understood ‘git’ and ‘svn’, they would think “I can probably help this person”. Below is the full question:

<img class="ui medium left circular floated image" src="../images/Stack_Overflow_logo.svg.png">

*I've been wondering whether there is a good "git export" solution that creates a copy of a tree without the .git repository directory. There are at least three methods I know of:*

*1.	git clone followed by removing the .git repository directory.*

*2.	git checkout-index alludes to this functionality but starts with "Just read the desired tree into the index..." which I'm not entirely sure how to do.*

*3.	git-export is a third party script that essentially does a git clone into a temporary location followed by rsync --exclude='.git' into the final destination.*

*None of these solutions really strike me as being satisfactory. The closest one to svn export might be option 1, because both those require the target directory to be empty first. But option 2 seems even better, assuming I can figure out what it means to read a tree into the index.*


The questioner asks the question with a goal posted, is concise, and lists what the questioner already knows. The question was very short although some code was included in it.

All the responses to the question were direct suggestions on how to export ‘git’ without a repository. They were 29 direct answers, and many discussions on those answers. Everyone was polite and professional, and contributed a lot to the topic.

<a href="http://stackoverflow.com/questions/160608/do-a-git-export-like-svn-export/163769#163769"><i class=""></i>View the StackOverflow question</a>

## Stupid question = Stupid answer
Now is an example of a question that did not fulfill the precepts for being a smart question. The question title is “how can I check if a given instance of a class belongs to the main class in python?” with the ‘python’ tag:

<img class="ui medium right floated image" src="../images/laptop.jpg">

*suppose you have:*

class F:

    pass
    
*then you make an instance:*

g=F()

*how can i check if the instance g is derived from the main class F?*

The first precept that was violated was the proper use of grammar. The lack of capitalizing on the first letter in the question and on the ‘I’ gives me the impression that the questioner is not to be taken seriously. The question itself was not very informative. Three lines of code were written, and by reading it, it appears to answer itself, so the reader does not understand what the questioner is trying to get at. If there was a clear goal put out, then the readers may have been more able to give a concise answer.

There were only 2 responses to the question. The first one who responded to this question made remarks like “Your question is confusing”, and contained questions to clarify what is being asked. Another reply gave an answer which to me did not seem like it was what the questioner was looking for. The question itself got marked as a Duplicate, meaning that if the author conducted a reasonable search, Stack Overflow would have come up with an answer directly pertaining to the question.

<a href="http://stackoverflow.com/questions/36042983/how-can-i-check-if-a-given-instance-of-a-class-belongs-to-a-main-class-in-python?noredirect=1&lq=1"><i class=""></i>View the StackOverflow question</a>

<img class="ui tiny circular left floated image" src="../images/yoda.jpg">

## Question smartly you should

The purpose of these examples is to show you what a good and bad question can look like.   The online forums of software engineers are full of people who would love to share their knowledge with you. Think carefully on the question before sending it out, and write it out with as much detail as possible. 


To learn more on asking smart questions, visit this awesome site by <a href="http://www.catb.org/esr/faqs/smart-questions.html"><i class=" "></i>Raymond and Moen</a>
