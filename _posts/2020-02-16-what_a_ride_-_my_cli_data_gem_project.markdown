---
layout: post
title:      "Pride Goes Before Destruction"
date:       2020-02-16 22:57:25 -0500
permalink:  what_a_ride_-_my_cli_data_gem_project
---

With over two weeks to complete my first project - a CLI Data Gem - I jumped in early with the intention of making a complex interface that I could eventually incorporate into another idea I had. I intended to have my CLI scrape multiple job boards. The problem I ran into, was I couldn't scrape everything the way I wanted to. So I defaulted to indeed.com since their website allowed for flexible search terms which would allow my CLI to have greater functionality.

# Scraping the Data
Indeed.com has a fairly simple data structure for scraping job data compared to other sites. It would allow multiple ways to search job data (city, state, zip) which made it easy to when figuring out the types of inputs I would need to capture from users.

Once I had an outline of how my project would operate, I began testing my scraping on repl.it. I wanted to capture a job by its title, company, the date it was posted, and the url for the job posting. A user would input where they wanted to search for jobs and they would be shown approximately 15 jobs (Indeed has about 5 sponsored postings that change each time the page reloads) from which they would select a job and receive a brief summary about it. This would be accomplished by scraping the specific job page by scraping data from the job-specific url.

I captured my `.css` elements and they were being returned the way I wanted on repl.it. I began setting up my environment on VS Code with `bundle gem install` so I could begin building my gem. 

# Scrapping the Scraper
I put together my `Scraper` and `Job` classes and modified the rest of my files. I built a simple CLI and thought I was basically done with the project in a few hours. I had some issues displaying the jobs the way I wanted to. I determined there was something wrong with how my data was being scraped and I decided I had plenty of time to figure it out and would spend the next few days reading more about scraping.

Then, I found out my wife's grandfather was in the hospital experiencing complications from a recent surgery.  Between that and some issues with work, my routine got messed up. Then things got worse with my grandfather-in-law and we were starting to make plans for a funeral. Next thing you know, a week and a half had passed and I was no closer to solving some of the issues with my `Scraper`.

With the funeral behind me and the Sunday deadline a little over 48 hours away, I gave my idea one last chance. I got my data displaying in a way I could work with, and began building out the rest of my CLI so that it would be functional for a user. After about an hour and a half of playing with different methods to manipulate my data, my `Job.title` data stopped displaying correctly. This meant that a user could not see the first level of data to select from. I tried to troubleshoot, but was staring down a deadline. I decided to trash my files and start over.

# Building an API
When I was able to continue working on this project, I had about 26 hours before it had to be submitted. I knew that I was going to have to work fast, and grabbing data from an API was going to be the path of least resistance for me. GitHub has a list of public APIs available at [here](https://github.com/public-apis/public-apis) and I began looking for something that did not require a key and had a straightforward application. I found the [NFL Arrests API](http://nflarrest.com/api/) and saw that it had a really easy interface to grab data.

I decided to pull data from the data set that had descriptions of crimes because I thought it would be fun to see what a professional athlete was arrested for. The API provides the data like this:
```
[{"arrest_stats_id":"35","Date":"2014-10-13","Team":"DAL","Team_name":"Cowboys","Team_preffered_name":"Dallas Cowboys","Team_city":"Dallas","Team_logo_id":"9","Team_Conference":"NFC","Team_Division":"East","Team_Conference_Division":"NFC East","Team_hex_color":"041E42","Team_hex_alt_color":"7F9695","reddit_group_id":"5","Name":"Joseph Randle","Position":"RB","Position_name":"Running Back","Position_type":"O","Encounter":"Arrested","Category":"Theft","Crime_category":"Theft \/ Burglary","Crime_category_color":"154F78","Description":"Accused of shoplifting at store in Frisco, Texas, after allegedly being caught in the act on video.","Outcome":"Pleaded guilty to misdemeanor, probation, $706 in costs. Charge could be dismissed if he stays out of trouble.","Season":"2014","ArrestSeasonState":"InSeason","overall_category_id":"9","general_category_id":"9","legal_level_id":"1","resolution_category_id":"1","Year":"2014","Month":"10","Day":"13","Day_of_Week":"Monday","Day_of_Week_int":"2","YearToDate":"0","DaysSince":"1934","DaysToLastArrest":"8","DaysToLastCrimeArrest":"1215","DaysToLastTeamArrest":"629"},{"arrest_stats_id":"213","Date":"2011-06-16","Team":"SEA","Team_name":"Seahawks","Team_preffered_name":"Seattle Seahawks","Team_city":"Seattle","Team_logo_id":"28","Team_Conference":"NFC","Team_Division":"West","Team_Conference_Division":"NFC West","Team_hex_color":"001433","Team_hex_alt_color":"4DFF00","reddit_group_id":"1","Name":"Raheem Brock","Position":"DE","Position_name":"Defensive End","Position_type":"D","Encounter":"Arrested","Category":"Theft","Crime_category":"Theft \/ Burglary","Crime_category_color":"154F78","Description":"Accused of walking out on $27 restaurant tab in Philadelphia. He said they canceled order before food arrived.","Outcome":"Acquitted.","Season":"2011","ArrestSeasonState":"OffSeason","overall_category_id":"9","general_category_id":"9","legal_level_id":"1","resolution_category_id":"4","Year":"2011","Month":"6","Day":"16","Day_of_Week":"Thursday","Day_of_Week_int":"5","YearToDate":"0","DaysSince":"3149","DaysToLastArrest":"0","DaysToLastCrimeArrest":"25","DaysToLastTeamArrest":"215"}
```

This seemed to have data I could use to satisfy the project requirements so I decided to use only a few of the available data points. Using `rest-client` to get the above data and parsing it with `JSON.parse` I could then iterate over the array and create new instances of the `Player` which would initialize with the attributes of `:Name, :Team_preffered_name, :Team_city, :Position_name, :Season, :Description, :Outcome, :DaysSince`. 

# Building the CLI
With the `Player` class built, I could build the `CLI` class to interface with a user. The each instance of the `Player` player class that was instantiated from the API's data was outputting to the user as intended. I ran into a few errors with my `Player` class' `attr_accessor`. I determined this was because I had used `:name` instead of `:Name`, which is how the API's `hash` `keys` were provided.

# Final Thoughts
I had big dreams for this project. I felt like I understood everything up to this point of the course curriculum and wanted to knock it out of the park with this project. Maybe I could have, or maybe I would have never figured out the issues with my `Scraper` in the time I had. But life gets in the way, and (in a sense) I'm glad I had to start over. I had to throw out all of my ideas and just write a basic workable CLI program. There was no time to be spending hours on stackoverflow or youtube to figure out things I haven't been taught. After all of the stress outside of this program the past two weeks,  I felt really good that I could knock out this project like I've been programming for years. 
