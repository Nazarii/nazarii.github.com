---
layout: post
title: "Make SQL query looks nice"
date: 2013-12-29 15:19
comments: true
categories: Tools
---
Found nice resource for SQL formatting: http://sqlformat.appspot.com/ . Service allows you to get nice SQL output from existing query quickly<!--more-->, so formatting:
{% codeblock SQL%}
select *
from foo
join bar on val1 = val2
where id = 123;
{% endcodeblock %}
will result in
{% codeblock SQL%}
SELECT *
FROM foo
JOIN bar ON val1 = val2
WHERE id = 123;
{% endcodeblock %}
which looks nice and more readable, especially when you have long queries.
Basicly service is demonstration of Python library python-sqlparse which is more pleasant. Enjoy it!