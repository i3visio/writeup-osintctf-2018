Level 6: Zambia
===============

Description
-----------

I have been shuttling teams. In 2007 we stood 4th in Euro cup for Counterstrike. I was on the team, can you find my ID?

**Points**: 200

WriteUp
-------

The first step is again to know with what kind of information we are dealing with. `Counterstrike` refers officially to `Counter-Strike` which can be also written as `Counter Strike`. Its a well-known videogame in the gaming-scene for which competitions have been held for many years. 

A quick Google Search `"Euro cup" "counter strike" 2007` throws several interesting results in the Liquipedia. It's a matter of trying to find the competition of Counter Strike held in 2007 which is the [EuroCup XV](https://liquipedia.net/counterstrike/EuroCup_XV).

![Eurocup](/res/level_06-eurocup.png)

The fourth team in that competition was formed by 5 guys from Denmark as follows.

![The members of the team](/res/level_06-mirror.png)

The obvious guess was trying to the following flags:
```

flag:{anizz}
flag:{caution}
flag:{Friis}
flag:{Lapez}
flag:{trace}
```

None of them were correct, (even capitalized ;)). By checking the two members with a Liquipedia website, [Friis](https://liquipedia.net/counterstrike/Friis) and [Trace](https://liquipedia.net/counterstrike/trace), we were luckier. Trace was also known as `spore'11`. So it was a matter of trying it:

```
flag{spore'11}
```

No luck with him, Fortunately, it was the other member who gave us the flag since Friis which was a. k. a. `fR11$HA` as shows [his page](https://liquipedia.net/counterstrike/Friis). Another challenge solved

![Friis profile page](/res/level_06-eurocup.png)

Solution
--------

`flag:{fR11$HA}`

Lessons Learned
----------------

The analyst arsenal for this challenge included:

- Google search engine

Things not to forget in future competitions:

1. Planification phase is always relevant so as to start to know where to start from. Google searches should be oriented to understand the information you are provided.
2. The search for alternative names is crucial. We have to consider to what extent the original data can be misspelled (it may not be the same `Euro Cup` than `Eurocup`, e. g.) or if it is part of the test. The interesting part is always that which is more special so as to minimize *infoxication* when possible in beforehand, i. e., long hashes, strange names and so on. 
3. It's always important to keep track of the flags already tested to avoid frustration and entering a vicius cyrcle.

