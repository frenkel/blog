---
layout: post
title: "PostgreSQL generate_series"
date: 2021-04-22 14:05:40 +0200
comments: true
categories: Programming
---

Ever needed to aggregate data per time period where you didn't have data points in every part of the period? I did when building [Callcounter](https://callcounter.eu). I wanted to generate a chart of requests per hour, where I didn't have requests in every hour. Using a naive PostgreSQL query I ended up with results such as this:

<pre>
=> SELECT date_trunc('hour', created_at),
-> COUNT(*) FROM events GROUP BY 1 LIMIT 10;

     date_trunc      | count 
---------------------+-------
 2021-03-22 10:00:00 |    32
 2021-03-22 11:00:00 |    92
 2021-03-22 13:00:00 |   213
 2021-03-22 14:00:00 |   237
 2021-03-22 16:00:00 |   331
 2021-03-22 17:00:00 |   389
 2021-03-22 18:00:00 |   452
 2021-03-22 19:00:00 |   493
 2021-03-22 20:00:00 |   273
 2021-03-22 21:00:00 |   152
(10 rows)
</pre>

Clearly there is no data for 12:00-13:59 and 15:00-15:59 in the database. Wouldn't it be great if we can fix this at the database level? That's where the [PostgreSQL `generate_series()` function](https://www.postgresql.org/docs/13/functions-srf.html) comes into play. We can use it to generate a consecutive range of items, which we can then join with our events table.

<pre>
=> SELECT * FROM generate_series('2021-04-22 10:00'::timestamp,
-> '2021-04-22 21:00', '1 hours');

   generate_series   
---------------------
 2021-04-22 10:00:00
 2021-04-22 11:00:00
 2021-04-22 12:00:00
 2021-04-22 13:00:00
 2021-04-22 14:00:00
 2021-04-22 15:00:00
 2021-04-22 16:00:00
 2021-04-22 17:00:00
 2021-04-22 18:00:00
 2021-04-22 19:00:00
 2021-04-22 20:00:00
 2021-04-22 21:00:00
(12 rows)
</pre>

Depending on the ORM you're using you'll need to find out how to join this with your events. Let me know on [Twitter](https://twitter.com/webindie_nl) if you're also interested in the ActiveRecord solution I chose.
