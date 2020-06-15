---
layout: post
title:      "Seeing the Forest Through the Trees - The Rails Project"
date:       2020-06-14 23:58:04 -0400
permalink:  seeing_the_forest_through_the_trees_-_the_rails
---


There is a lot of things Rails can do and it's tempting to get bogged down in all of the gems and YouTube videos. As a person that is new to programming, I found this to be overwhelming for this specific project.

## Plan Your Work and Work Your Plan

I started this Rails project with an idea that I've been working on since the Sinatra project and was pumped to harness the power of Rails. I would take some of the basics of my Sinatra project, refactor things for Rails, and then start exploring all of the gems out there that could do the things that would make this a viable product. Except, I didn't sit down and fully map my ideas. This lead to a host of problems and inefficient work. I was constantly going back through my views to make changes, I spent too much time on page styling (only to just delete almost all of it), and wasted about 5 days playing around with things that probably did not need to be touched. Knowing how much of a headache trying to style the front end without really knowing a ton of css or any javascript, I quickly realized that trying to jump write into coding is a terrible idea. There must be clear objectives broken down in workable chunks.

## Rails "Magic" Isn't Wizard Powers
The problem with "Rails Magic" is that it's easy for new programmers to fall into and think they know what is going on under the hood. In my month or so dive into learing Rails, I started feeling like I understood everything. Until I was trying to delete an object. I had a bug with my migrations. I don't even think about migrations anymore because it seems so simple. Yet, I generated my migrations using a generator, and set up model associations, controllers, and views without using a generator.

I did a ```db:migrate``` and everything seemed fine. I continued on and set up all of the CRUD actions, and everything worked until I got to ```destroy```. Logs showed that ActiveRecord was rolling back the transaction and nothing was being deleted. I read the docs, added ```dependent: :destroy``` where it needed to go and it still was not working. After the better part of a day, I decided to just delete all of my migrations and write them all myself. That seemed to fix the instant problem. 

The core problem is relying on Rails to do the work for you. A good example is authentication. I spent about a day working with the Devise gem after I had already set up a simple email and password authentication that worked. I followed every instruction on multiple sites and still couldn't get it to work the way I wanted it to. Perhaps it would have been easier to start with Devise when I created my project. Instead, I let rails magic do its thing and it ended up being more of a headache.

This project actually made me feel like I knew less about rails than while I was working on labs. This is probably a good thing because being humbled by something is important for growth, but from now on I am going to outline my goals and research gems prior to even opening a terminal or text editor. Otherwise, the "man behind the curtain" which is rails will create bugs that will slow any progress down to a crawl. 
