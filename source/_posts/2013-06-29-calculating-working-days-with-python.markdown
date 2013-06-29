---
layout: post
title: "Calculating working days with python."
date: 2013-06-29 21:15
comments: true
categories: Python
---

So the specification is following:
{% blockquote %}
We need to calculate number of working days between two dates - it mean's we need to calculate all days excluding Saturday and Sunday. If the function is running after 6:00 pm this working day need to be also excluded.
{% endblockquote %}
<!-- more -->
After some googling I've found this task could be resolved using rrule module.
Be sure you have [dateutil](http://labix.org/python-dateutil) library installed to use this example.
{% codeblock sublime-text lang:python%}
import time
from dateutil import rrule

def get_working_days(date_start_obj, date_end_obj):
    weekdays = rrule.rrule(rrule.DAILY, byweekday=range(0, 5), dtstart=date_start_obj, until=date_end_obj)
    weekdays = len(list(weekdays))
    if int(time.strftime('%H')) >= 18:
        weekdays -= 1
    return weekdays
{% endcodeblock %}
Here byweekday parameter is a list of days of week we want to caculate, ti's elements can be integers (Monday is 0, Tuesday is 1 etc) or rrule objects - rrule.MO, rrule.TU etc. Other usefull methods for date (e.g. full weeks) calculations could be found [here](http://labix.org/python-dateutil).

Suppose we need to calculate days from 1-01-2013 until 28-07-2013.
Our code will be:
{% codeblock sublime-text lang:python%}
from datetime import date

date_start_obj = date(2013, 1, 1)
date_end_obj = date(2013, 7, 18)
print get_working_days(date_start_obj, date_end_obj):
{% endcodeblock %}
The output wil be: **142**