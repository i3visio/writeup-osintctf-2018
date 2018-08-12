Level 5: Guatemala
===================

Description
-----------

I got the gold css badge in Apr 2011. What is my post code?

**Points**: 300

WriteUp
-------

So, the first step is to try to guess what is a *gold CSS badge*. Mentioning CSS, the first idea is to go to Stackoverflow or sites in which web technologies are explained. I was lucky with Stackoverflow because it has a way of recognising the expertise of a user which answers a lot of questions in the website by awarding different badges being the *gold badge* a relevant one.

In the case of the *CSS gold badge* its a matter of fulfilling the requirements as described in [StackOverflow's help center](https://stackoverflow.com/help/badges/247):

*Earn at least 1000 total score for at least 200 non-community wiki answers in the css tag. These users can single-handedly mark css questions as duplicates and reopen them as needed.*

[Here](https://stackoverflow.com/help/badges/247?page=1) you can find a list of the users who fulfilled this task ordered by date of achievement (more recent, appear before) and [here, in the second page](https://stackoverflow.com/help/badges/247?page=2), we can find the first of the 2 users (just [BoltClock](https://stackoverflow.com/users/106224/boltclock) and [bobince](https://stackoverflow.com/users/18936/bobince)) who achieved the goal in April 2011.

![Profile created in April 2011](/res/level_05-april.png)


So it's a matter of finding where can we find a post code in the profile page of [BoltClock](https://stackoverflow.com/users/106224/boltclock):

![Capture of the profile page of BoltClock](/res/level_05-profile.png)

We can find there a lot of information about social media profiles (using `Novalistic` as a username). Extra information could be found in different profiles using `Novalistic` or `BoltClock` (such as his [Gravatar profile](http://es.gravatar.com/BoltClock.json) referencing back to novalistic.com and so on), but in this case getting access to the WhoIs data did the trick. The information available at [Whoisology](https://whoisology.com/novalistic.com) was enough.

![Whoisology data about novalistic.com](/res/level_05-novalistic.com.png)

Solution
--------

`flag:{520320}`

Lessons Learned
---------------

The analyst arsenal for this challenge included:

- Google search engine
- Stackoverflow
- Whoisology

Things not to forget in future competitions:

1. Planification phase is always relevant so as to start to know where to start from. Google searches should be oriented to understand the information you are provided.
2. For European based analysts it's important to understand the limitations of GDPR regarding WhoIs information and related data taking into account the current regulations. [Inteltechniques colleciton of domain searches](https://inteltechniques.com/menu.html) is always a good starting point so as to try to find alternative sources for domain data.
3. Have a good tool to find additional information about usernames and emails (maybe with [OSRFramework's usufy and mailfy](https://github.com/i3visio/osrframework)) to try to get additional information about the user *leaked* on different websites.
4. Understanding the question so as to try to guess what you are being asked for. Post code (for *postal code* in the case can be misleading and make you waste time) or even for post ID or similar. Just keep the focus.
