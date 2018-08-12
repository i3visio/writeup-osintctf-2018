Level 11: Ethiopia
==================

Description
-----------

```
While pen-testing an organization in Germany, our pen-tester figured out the redis build id, i.e. ef08edc3eb2339c3. He was trying to figure out the run id of the server to compromise it further. However, since the connectivity dropped, IP changed. Can you figure out the 'run_id' of this server.
```
**Points**: 100

WriteUp
-------

As what typically happends with similar challenges, having a very concret piece of data like the Redis build id is a good strating point. Let's start a search in Shdoan for it: `ef08edc3eb2339c3`.

Having no results is not a problem if you know how this data is shown by legitimate Redis servers. Let's look for `redis`.

So we have things like this:

![A Redis example](/res/level_11-redis_example.png)

Let's try `redis_build_id:ef08edc3eb2339c3`. The results are not a lot. 

![A lot of machines](/res/level_11-many_systems.png)

Remember that the description said that the pentesting took place in Germany, so let's add `country:"DE"`. 

![Looking for German machines](/res/level_11-germany.png)

It seems that it is time to try until we find the correct one `57109bb0e90558c7b83bbacb098811e22e87cfdb`. Another one for us.

Solution
--------

`flag:{57109bb0e90558c7b83bbacb098811e22e87cfdb}`

Lessons Learned
---------------

The analyst arsenal for this challenge included:

- Shodan (logged account)

Things not to forget in future competitions:

1. It's important to invest some time before the competition to keep track of your logged accounts in these services. Most of the times they have added features that can let you have more filter options and show more results.
2. Although unneded here, having a solid knowledge of advanced searching techniques will behelpful to dientify relevant keywords from the description.
3. Having a list of similar alternative tools to Shodan is important: alternatives include [Censys.io](https://censys.io) or [Zoomeye.org](http://zoomeye.org/).
3. Again, reading the rules at the beginning of the competition to know the flag submission format. And do not forget a single colon. Never.
