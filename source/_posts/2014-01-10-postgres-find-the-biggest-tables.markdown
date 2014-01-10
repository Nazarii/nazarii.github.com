---
layout: post
title: "Postgres: find the biggest tables"
date: 2014-01-10 21:18
comments: true
categories: Sql
---
Usefull query to find 20 biggest tables in your PostgreSQL database:<!--more-->
{% codeblock SQL%}
SELECT nspname || '.' || relname AS "relation",
    pg_size_pretty(pg_relation_size(C.oid)) AS "size"
  FROM pg_class C
  LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
  WHERE nspname NOT IN ('pg_catalog', 'information_schema')
  ORDER BY pg_relation_size(C.oid) DESC
  LIMIT 20;
{% endcodeblock %}