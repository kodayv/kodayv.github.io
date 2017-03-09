---
layout: essay
type: essay
title: "Meteor Gotchas"
date: 2017-03-09
labels:
  - Software Engineering
  - Meteor
---



## Spellslayer
During my latest Meteor experience, I was working on a form for my page. Things were going fairly smooth and I was on the code in which the validation of the user input to the form would occur. Then my form disappeared from the webpage. I was initially boggled with disbelief. How dare that page not load when it was just working fine a few minutes ago! Keeping my cool, I went to check on the page I was editing. First I checked to ensure that the page Foo was inputted. So far so good. Then I looked down the rest of the code: Foo is called, foo is used…what was wrong? Refusing to give up I pulled up the inspection element on the local page through Google Chrome. Behold, an error existed! That error was in the page I was already looking at. I was confused, I needed coffee. Upon obtaining a +2 elixir of intellect (as coffee has been claimed to be), I looked at the error note again; ‘file/foo does not exist’. Then it dawned on me, the file was called ‘foos’! After brandishing myself for overlooking such a crucial detail, I was able to make all my changes to foo and the page returned, once again, to its glory.

## Whipping the Turtle
Meteor is a really good program for creating complex web pages. My only grievance in this program is its inability to swiftly start up the page. When initially running meteor on code, I have experienced a wait time of over 30 minutes. That means that I have already made and finished my coffee, began the initial part of my code, and have read today’s news reports and am still waiting to actually get to work! I have found this extremely frustrating (albeit that may be largely due to what the media is currently reporting on). Naturally I looked up sources on making the build faster. The first recommendation for running the program on Windows is to temporarily disable the Windows firewall. As a user of BitDefender, my Windows firewall is already disabled, and BitDefender is a little tricky to work around. It would tell me that it is not automatically screening, and then approximately 50% of the time I run meteor would ask me if I give the program permission to run. I attempted to add meteor as a permitted site, but the occasional popup would still happen. I do not know if this random interjection is permission is for a download that happens occasionally, or if BitDefender only works 50% of the time. It is my hope that the former is true, but I do not know how to diagnose such an occurrence. 
