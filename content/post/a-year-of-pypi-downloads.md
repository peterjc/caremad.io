---
title: A Year of PyPI Downloads
date: 2015-04-20
---

A little over a year ago we started archiving all of the logs generated by
PyPI and today we'll take a look at these logs to see how various things have
changed in that time. This data comes from parsing the user agents of the
tools downloading files from PyPI and because of that it's reliability is
dependent on the reliability of that data.

First we'll take a look at how PyPI has grown over the last year:

![Total Downloads](/images/a-year-of-pypi-downloads/area-total-downloads.png)

This graph shows how many files were downloaded from PyPI in a one week period
of time, as you can see in January of 2014 that number was roughly 12 million
downloads a week, and now in April of 2015 that number has grown to roughly 35
million, a growth rate of roughly 300%.

Next let's take a look at what people are using to download these files, this
could be their browser, mirroring clients such as
[bandersnatch](https://pypi.python.org/pypi/bandersnatch), or through an
installer such as [pip](https://pip.pypa.io/).

![Installer Traffic](/images/a-year-of-pypi-downloads/stacked-installer-pct.png)

We can see from this chart that pip is by far the most popular method of
downloading files from PyPI with a share of roughly approximately 70% of all of
the downloads from PyPI and that while distribute still has a small number of
users, it has rapidly been declining into (hopefully) nothing. We can also see
that almost none of the downloads are initiated by a browser, indicating that
everyone is using some sort of automated download or installer to fetch files
from PyPI. Another interesting thing to notice is that the mirroring protocol
accounts for roughly 20% of all of the traffic on PyPI although we have no way
of determining what the traffic looks like to those mirrors, so they may
actually represent more (or less) than 20% of the actual traffic.

Now we're going to move into data which is going to have varying degrees of
complete-ness. Since all of this data comes from parsing the request logs of
PyPI we can only know what is included in the HTTP requests made to PyPI.
Historically pip used the default urllib2 user-agent of ``Python-urllib2/X.Y``
and setuptools uses a slightly modified urllib2 user-agent that also includes
that fact that it is setuptools, and what version of setuptools it is. Recent
versions of pip (starting with 1.4) have each added slightly more information
to the user-agent which enables us to gain a more detailed view into what sort
of environments are reaching out to PyPI. Given that pip accounts for roughly
70% of the downloads this gives us a decent view into the nature of the
traffic.

Let's take a look at what versions of pip are in play, this will give us some
hints as to what features we can expect users of PyPI to have.

![pip Versions](/images/a-year-of-pypi-downloads/stacked-pip-ver-pct.png)

In this graph, the "Unknown" value typically represents versions of pip older
that 1.4 (when pip first started identifying itself in it's user-agent),
however because it was simply using the default user-agent it could just as
easily be another utility that also used urllib2 with the default user-agent.

Looking closer at the graph, we can see that ~60% of the pip users will install
wheels by default and that roughly 35% of pip users will be caching their
downloads from PyPI by default.

The Wheel format is a binary distribution format which is understood by pip,
it offers several improvements over the older Egg format and it is generally
regarded as the way forward for binary distribution on PyPI. Let's take a look
at how many of the downloads from PyPI were downloading a Wheel file versus
other kinds of distribution types.

![Distribution Types](/images/a-year-of-pypi-downloads/stacked-dist-pct.png)

A year later Wheels have gone from a tiny fraction of the total downloads of
PyPI to nearly 20% on their own and in that same time Eggs have gone from ~5%
to ~2-3%. This indicates that Wheels are reaching people who would have
previously had to install directly from a source distribution.

Finally let's take a look at what is probably the question which everyone is
wondering, what versions of Python are downloading files from PyPI?

![All Python Versions](/images/a-year-of-pypi-downloads/stacked-py-pct.png)

![All Python 3.x Versions](/images/a-year-of-pypi-downloads/stacked-py3-pct.png)

This particular set of data is some of the most complete, every installer has
indicated at least the major and minor version (``X.Y``) of the language
(specifically the language, not the interpreter's version). These two graphs
show the same data, the second is simply zoomed in on only the 3.x versions of
Python.

Looking at these graphs, we can see that in the past year Python 3.x has grown
from roughly 2% of the total downloads from PyPI to roughly 5-6%. For authors
wondering what versions of Python 3.x they should support, it's easy to make
the argument that targeting 3.4, or at the very least 3.3 is a completely
reasonable target given that 3.2 (and to a lesser extent, 3.3) have a very tiny
marketshare which very likely mostly consists of automated CI systems. Another
interesting observation from these graphs is that the usage of 2.6 has more or
less remained consistent with perhaps a slight decline.

For the Python 3 enthusiasts out there, things are not necessarily as bleak as
they might seem. When we restrict our view of the data to specific projects we
can get vastly different results. One striking example that I've noticed was
the [Django](https://www.djangoproject.com/) project.

![Django Python Versions](/images/a-year-of-pypi-downloads/django-stacked-py-pct.png)

In this graph we can see that Django has grown to an almost 20% of it's
downloads coming from Python 3. When looking across other web frameworks such
as [Flask](http://flask.pocoo.org/) and
[Pyramid](http://www.pylonsproject.org/) we can see similar numbers of Python 3
support.

Leaving the world of web frameworks and taking a look at one of the most
popular downloads on PyPI, let's take a look at what versions of Python are
downloading [requests](http://python-requests.org/).

![requests Python Versions](/images/a-year-of-pypi-downloads/requests-stacked-py-pct.png)

With requests we can see that roughly 6-7% of the downloads are Python 3, which
is a slight increase from the global numbers of 5-6% but only slightly so.
