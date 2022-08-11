# Peer-Grade-Page-Rank-Project
Simple Python Search Spider, Page Ranker, and Visualizer

This is a set of programs that emulate some of the functions of a 
search engine.  They store their data in a SQLITE3 database named
'spider.sqlite'.  This file can be removed at any time to restart the
process.

You should install the SQLite browser to view and modify 
the databases from:

http://sqlitebrowser.org/

This program crawls a web site and pulls a series of pages into the
database, recording the links between pages.

Note: Windows has difficulty in displaying UTF-8 characters
in the console so for each console window you open, you may need
to type the following command before running this code:

    chcp 65001

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how

Mac: rm spider.sqlite

Mac: python3 spider.py

Win: del spider.sqlite

Win: spider.py

Enter web url or enter: http://www.dr-chuck.com/


['http://www.dr-chuck.com']

How many pages:2

1 http://www.dr-chuck.com/ 12

2 http://www.dr-chuck.com/csev-blog/ 57

How many pages:

In this sample run, we told it to crawl a website and retrieve two 
pages.  If you restart the program again and tell it to crawl more
pages, it will not re-crawl any pages already in the database.  Upon 
restart it goes to a random non-crawled page and starts there.  So 
each successive run of spider.py is additive.

Mac: python3 spider.py 
Win: spider.py

Enter web url or enter: http://www.dr-chuck.com/

['http://www.dr-chuck.com']

How many pages:3

3 http://www.dr-chuck.com/csev-blog 57

4 http://www.dr-chuck.com/dr-chuck/resume/speaking.htm 1

5 http://www.dr-chuck.com/dr-chuck/resume/index.htm 13

How many pages:

You can have multiple starting points in the same database - 
within the program these are called "webs".   The spider
chooses randomly amongst all non-visited links across all
the webs.

If you want to dump the contents of the spider.sqlite file, you can 
run spdump.py as follows:

Mac: python3 spdump.py 
Win: spdump.py
(5, None, 1.0, 3, u'http://www.dr-chuck.com/csev-blog')

(3, None, 1.0, 4, u'http://www.dr-chuck.com/dr-chuck/resume/speaking.htm')

(1, None, 1.0, 2, u'http://www.dr-chuck.com/csev-blog/')

(1, None, 1.0, 5, u'http://www.dr-chuck.com/dr-chuck/resume/index.htm')
4 rows.

This shows the number of incoming links, the old page rank, the new page
rank, the id of the page, and the url of the page.  The spdump.py program
only shows pages that have at least one incoming link to them.

Once you have a few pages in the database, you can run Page Rank on the
pages using the sprank.py program.  You simply tell it how many Page
Rank iterations to run.

Mac: python3 sprank.py 
Win: sprank.py 

How many iterations:2
1 0.546848992536

2 0.226714939664

[(1, 0.559), (2, 0.659), (3, 0.985), (4, 2.135), (5, 0.659)]

You can dump the database again to see that page rank has been updated:

Mac: python3 spdump.py 
Win: spdump.py 
(5, 1.0, 0.985, 3, u'http://www.dr-chuck.com/csev-blog')

(3, 1.0, 2.135, 4, u'http://www.dr-chuck.com/dr-chuck/resume/speaking.htm')

(1, 1.0, 0.659, 2, u'http://www.dr-chuck.com/csev-blog/')

(1, 1.0, 0.659, 5, u'http://www.dr-chuck.com/dr-chuck/resume/index.htm')

4 rows.

You can run sprank.py as many times as you like and it will simply refine
the page rank the more times you run it.  You can even run sprank.py a few times
and then go spider a few more pages sith spider.py and then run sprank.py
to converge the page ranks.

If you want to restart the Page Rank calculations without re-spidering the 
web pages, you can use spreset.py

Mac: python3 spreset.py 
Win: spreset.py 

All pages set to a rank of 1.0

Mac: python3 sprank.py 
Win: sprank.py 

How many iterations:50
1 0.546848992536

2 0.226714939664

3 0.0659516187242

4 0.0244199333

5 0.0102096489546

6 0.00610244329379
...
42 0.000109076928206

43 9.91987599002e-05

44 9.02151706798e-05

45 8.20451504471e-05

46 7.46150183837e-05

47 6.7857770908e-05

48 6.17124694224e-05

49 5.61236959327e-05

50 5.10410499467e-05

[(512, 0.02963718031139026), (1, 12.790786721866658), (2, 28.939418898678284), (3, 6.808468390725946), (4, 13.469889092397006)]

For each iteration of the page rank algorithm it prints the average
change per page of the page rank.   The network initially is quite 
unbalanced and so the individual page ranks are changing wildly.
But in a few short iterations, the page rank converges.  You 
should run prank.py long enough that the page ranks converge.

If you want to visualize the current top pages in terms of page rank,
run spjson.py to write the pages out in JSON format to be viewed in a
web browser.

Mac: python3 spjson.py 

Win: spjson.py 

Creating JSON output on spider.js...
How many nodes? 30
Open force.html in a browser to view the visualization

You can view this data by opening the file force.html in your web browser.  
This shows an automatic layout of the nodes and links.  You can click and 
drag any node and you can also double click on a node to find the URL
that is represented by the node.

NOTES       : If your python compiler version is up to 3.8 you must delete folder bs4 and you can install in terminal 
pip install beautifulsoup4

ASSIGNMENT  : First you will spider 100 pages from http://python-data.dr-chuck.net/ run the page rank algorithm and take some screen shots. Then you will reset the spider process and spider 100 pages from any other site on the Internet, run the page rank algorithm, and take some screen shots.

SOLUTION    :

A ) Spider 100 pages from http://python-data.dr-chuck.net/
1. Image of output spider.py
![1](https://user-images.githubusercontent.com/89823572/184090933-d1b4678d-2591-4b5b-a643-008a5b427769.jpg)
![2](https://user-images.githubusercontent.com/89823572/184090961-f2c64cbb-f1b3-4afd-9170-e6e45604ec5b.jpg)

2. Image of output spjson.py
![4](https://user-images.githubusercontent.com/89823572/184091778-78686d0c-db45-46cc-9a63-9a551fae83f7.jpg)

3. Image of output spdump.py
![3 ](https://user-images.githubusercontent.com/89823572/184092932-2b6d8167-6b6a-499e-bfed-3c8747cc5149.jpg)


4. Screenshoot of force.html
![3](https://user-images.githubusercontent.com/89823572/184092832-f3890a3f-2d79-4e5b-b659-893b1d4d2b46.jpg)

A ) Spider 100 pages from http://python-data.dr-chuck.net/
1. Image of output spider.py
![2](https://user-images.githubusercontent.com/89823572/184143418-3b129758-1323-4786-89b8-227fe5b66209.jpg)
![3 ](https://user-images.githubusercontent.com/89823572/184143442-c8d92e12-eda8-492e-b569-820fb606f4f8.jpg)


2. Image of output spjson.py
![4](https://user-images.githubusercontent.com/89823572/184091778-78686d0c-db45-46cc-9a63-9a551fae83f7.jpg)

3. Image of output spdump.py
![1](https://user-images.githubusercontent.com/89823572/184143485-d4b2984b-8af8-48c4-92ed-06c286d4170e.jpg)
![5](https://user-images.githubusercontent.com/89823572/184143923-488be0be-b0c7-41bf-97cf-a239970fb92d.jpg)
![7](https://user-images.githubusercontent.com/89823572/184145665-d8e47509-a576-4a1f-acd1-d0fb069805d8.jpg)



4. Screenshoot of force.html
![8](https://user-images.githubusercontent.com/89823572/184145896-19dad72f-d10b-4d8e-b373-fc7ba299f4d6.jpg)

