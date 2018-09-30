---
layout: post
title: Recycle ideas - how to use cool ideas in a legacy project
excerpt: "How to use cool ideas in a legacy project - take the most of blogpost, conference talks and use it on your advantage"
tags: [code, architecture, methods]
modified: 2018-09-24
comments: true
---

Working on legacy projects is hard. Is even harder, when your boss or coworkers are sticking to the ways they know the most and do not want to experiment or try new things. And - after a while of coding - I'm sure not every new hyped idea is worth pursuing and every new gem is not worth introducing. Now I feel that slim gemfile in a ruby project is actually a good indicator of a healthy code and I would be very careful with projects that implement all of the new shiny things.


But it does not mean that I say no to the new tools coming my way and just ignore them altogether. It means I'm extremely interested, but less in using a new library or gem, but more in the IDEAS behind it. What problems have authors wanted to solve? In which way? Why they have chosen this path over different one? And I try to get into the mindset of: which of this ideas I can use in my projects? Which make sense? Is there any idea that solves a problem we are currently facing? Is there anything I can do to make the code better than I just have learned?


Sometimes just a part of the new framework may be a solution or you can start only with a part of the big architecture paradigm. There are things that can be used NOW, tomorrow, in your next pull-request. I want to show how I incorporated new ideas that I learned into Ruby on Rails projects, what inspired me and if I have needed to face any opposition.


### Operations.

  When I was a junior developer, I had MVC model in my head all the time. With not that much guidance, it was hard for me to break from this pattern. Once I decided to read the Trailblazer book it has changed. I found out that I can use more than models and controllers to store business logic in the app and how to do it. I started to put a code into a set of classes I called `actions`, they were responsible for business logic that otherwise would be in the controller. All creating new records, handling more complicated actions, generally speaking, I moved the code that in rails way would be in controller and split it into small, easily testable in isolation chunks. It actually had a little bit of a snowball effect, other developers started using this pattern as well, what resulted in cleaner, easier to maintain code throughout the application.


### Hanami style-controllers
  In typical Ruby on Rails application controllers have this tendency to grow in an uncontrolled way. Usually, it starts with the typical controller for a resource, with a couple of methods, but with every change, with every additional business logic, controller grows. We end up with the controller with over 200 LoC, in which every method is connected with different action, that is so hard to test or develop further. One of the ways to prevent this kind of situations is to divide this overgrown controller into smaller ones - controller per action strategy. This strategy was adopted by authors of Hanami framework, quite new and interesting alternative for Rails.
  This way, a controller stops being a big ball of mixed up methods, but is strictly connected and has one reason to change, so fulfills Single Responsibility Principle.
  Of course, this solution often raises voices about routes looking weird, but if it’s the only cost of having a more organized code, for me it’s the price worth paying.


### DDD
  Domain-driven design is probably the most complex and most advanced of examples I have presented. I’m not going to even try to explain this huge idea here, there are more articles and books about it that would do a much better job than me. But there are solutions that can be used immediately and without any revolution in any current project.
  The first idea is to use common language throughout the app. And by the common language, I understand terms that are widely understood not only in developers team but in all teams, marketing, sales, whichever team belongs to the company. Good understanding of the product, all business surrounding it is crucial not only for financial success but for technical as well. Being able to foreseen problems is so much harder when you cannot see the full picture.


  The second part is a little bit harder, but still manageable even in the legacy Rails app. It’s separating all logic connected to one topic - not Active-Record model, but a chunk of code responsible for one thing into one or set of classes, if it’s bigger, and calling it only through this domain class. So, for example, if in the app there is a possibility to exchange messages between users, but it also triggers some kind of notifications and other actions, it would be beneficial to hide this logic in one place and request any actions on messages only through the domain. It allows to refactor code only in one place and, if in the future, there will be a decision to extract messages into the microservice, it will require changing only the code in the domain, rest of the app would be left untouched and still working.

## To sum up...
I was trying to prove that we do not need to incorporate all of the new ideas into the app we are working on, we can pick and choose and try whatever works best for us. It is sometimes hard to work with the legacy app, but a good understanding of the problem and finding a solution for this particular issue is, in my opinion, a key to the success.
