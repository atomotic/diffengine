<div style="text: center;">
<img height="200" src="https://github.com/DocNow/diffengine/blob/master/diffengine.png?raw=true">
</div>

diffengine is a utility for watching RSS feeds to see when story content
changes. When new content is found a snapshot is saved at the Internet Archive,
and a diff is generated for sending to social media. The hope is that it can
help draw attention to the way news is being shaped on the web. It also creates
a database of changes over time that can be useful for research purposes.

diffengine draws heavily on the inspiration of [NYTDiff] and [NewsDiffs] which
*almost* did what we wanted. [NYTdiff] is able to create presentable diff images
and tweet them, but was designed to work specifically with the NYTimes API.
NewsDiffs provides a comprehensive framework for watching changes on multiple
sites (Washington Post, New York Times, CNN, BBC, etc) but you need to be a
programmer to add a [parser
module](https://github.com/ecprice/newsdiffs/tree/master/parsers) for a website
that you want to monitor. It is also full on website which involves some
commitment to install and run.

With the help of [feedparser] diffengine takes a different approach of working
with any site that publishes an RSS feed of changes. This covers many news
organizations, but also personal blogs and organizational websites that put out
regular updates. And with the [readability] module diffengine is able to
automatically extract the primary content of pages, without requiring special
parsing to remove boilerplate material. And like NYTDiff, instead of creating
another website for people to watch diffengine pushes updates out to social
media where people are already, while also building a local database of diffs
that can be used for research purposes.

## Install 

1. install [PhantomJS] - also, see [install examples]
1. install [Python 3]
1. `pip3 install --process-dependency-links diffengine`

*Coming soon: platform specific binaries.*

## Run

In order to run diffengine you need to pick a directory location where you can
store the diffengine configuration, database and diffs. For example I have a
directory in my home directory, but you can use whatever location you want, you
just need to be able to write to it.

The first time you run diffengine it will prompt you to enter an RSS or Atom
feed URL to monitor and will authenticate with Twitter. 

    % diffengine /home/ed/.diffengine 

    What RSS/Atom feed would you like to monitor? https://inkdroid.org/feed.xml

    Would you like to set up tweeting edits? [Y/n] Y

    Go to https://apps.twitter.com and create an application.

    What is the consumer key? <TWITTER_APP_KEY>

    What is the consumer secret? <TWITTER_APP_SECRET>

    Log in to https://twitter.com as the user you want to tweet as and hit enter.

    Visit https://api.twitter.com/oauth/authorize?oauth_token=NRW9BQAAAAAAyqBnAAXXYYlCL8g

    What is your PIN: 8675309

    Saved your configuration in /home/ed/.diffengine/config.yaml
    
    Fetching initial set of entries.

    Done!

After that you just need to put diffengine in your crontab to have it run
regularly, or you can run it manually at your own intervals if you want. Here's
my crontab to run every 30 minutes to look for new content.

    0,30 * * * * /usr/local/bin/diffengine /home/ed/.diffengine

You can examine your config file at any time and add/remove feeds as needed.  It
is the `config.yaml` file that is stored relative to the storage directory you
chose, so in my case `/home/ed/.diffengine/config.yaml`.

## Examples

* [wapo_diff]: edits to [The Washington Post]
* [breitbart_diff]: edits to [Breitbart News]
* [guardian_diff]: edits to [The Guardian]
* [torstar_diff]: edits to [The Toronto Star]
* [globemail_diff]: edits to the [The Globe and Mail]
* [canadaland_diff]: edits to [Canadaland]

## Develop

[![Build Status](https://travis-ci.org/DocNow/diffengine.svg)](http://travis-ci.org/DocNow/diffengine)

[nyt_diff]: https://twitter.com/nyt_diff
[NYTDiff]: https://github.com/j-e-d/NYTdiff
[NewsDiffs]: http://newsdiffs.org/
[feedparser]: https://pythonhosted.org/feedparser/
[readability]: https://github.com/buriy/python-readability
[PhantomJS]: http://phantomjs.org
[Python 3]: https://python.org
[install examples]: https://gist.github.com/julionc/7476620

[wapo_diff]: https://twitter.com/wapo_diff
[The Washington Post]: https://www.washingtonpost.com

[breitbart_diff]: https://twitter.com/breitbart_diff
[Breitbart News]: https://www.breitbart.com

[guardian_diff]: https://twitter.com/guardian_diff
[The Guardian]: https://www.theguardian.com/

[torstar_diff]: https://twitter.com/torstar_diff
[The Toronto Star]: https://www.thestar.com/

[globemail_diff]: https://twitter.com/globemail_diff
[The Globe and Mail]: http://www.theglobeandmail.com/

[canadaland_diff]: https://twitter.com/canadaland_diff
[Canadaland]: http://www.canadalandshow.com/
