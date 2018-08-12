Level 3: Sweden
===============

Description
-----------

```
A meeting happened at CSU Foothills Campus and one of the agenda was Mock Forecast. We suspect that someone was able to sneak into the meeting by figuring out the meeting id and access code somehow. Can you investigate if the Access code is being leaked somewhere. 
```
**Points**: 100

WriteUp
-------

An easy seach in Google for `"CSU Foothills Campus" "Mock Forecast"` throws [this](https://docs.google.com/spreadsheets/d/1Msa4mRWoX1jCPm0nSLcN2veYC0jXA6AnsTVG1JVXXJU/edit#gid=524742692) only result.

![Results thrown by Google](/res/level_03-google_results.png)


The Google Drive document shows an spreadsheet like the one that follows. It's just a matter of finding the word `code` (`Ctrl + F`).

![Capture of the spreadsheet](/res/level_03-google_doc.png)


Just keep track of the results inserted and check t hat the format is the appropriate. So as not to waste time as I did.


Solution
--------

`flag:{685-295-741}`

Lessons Learned
---------------

The analyst arsenal for this challenge included:

- Google Search Engine

Things not to forget in future competitions:

1. Identifying the relevant keywords in the description to start launching the queries.
2. Although unneded here, having a solid knowledge of advanced Google Dorking techniques.
3. Reading the rules at the beginning of the competition to know the flag submission format. And do not forget a single colon. Never.
