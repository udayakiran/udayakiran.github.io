---
layout: post
title: "Ruby/Rails - Database replication with rails4"
description: "Ruby/Rails - Support master-salve DB setup (replication) for active record 4 (rails 4)"
tags: [ruby, rails, performance, scalability]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

This is a quick write up about the options we looked at to implement master-salve DB setup (replication and failover) for active record 4 (rails 4).

- Our need was that all reads should go to slave and writes to master.

- Some critical reads should still go to master.

- There should be a flexibilty to decide which query should hit master and which one to hit slave.

## Options -

We were using [schoefmax's multi DB](https://github.com/schoefmax/multi_db) gem with rails 2 which is no more supported in rails 4. Did not make many attempts to fix it as we wanted to take the advantage of the optimizations and new query style added in Active Record 4 and implementing all of this with multi db is some effort.


The following gems are evaluated.

1.  <https://github.com/taskrabbit/makara> -
 - This is great. Automatically switches reads and writes in and can be overridden easily.
 - Dbs can be blacklisted.
 - Sticky flows can be maintainted.

2. <https://github.com/tchandy/octopus> -
 - This is very good. Code changes needed are very simple.
 - Supports sharding, replication and failover.
 - Does not seem to automatically switching reads and writes that well.

3. <https://github.com/wbharding/seamless_database_pool> -
 - This is good and does do well with replication and failover.
 - Not rails 4 compatible.


 Chose makara gem as it seems to exactly does what we need and is being maintained actively. Octopus would be preferred over this incase we decide to go with sharding in future.


## Implementation with makara gem -

### Enabling multiple DB support on any environment -

Change the database.yml like below. No code change is needed.

{% highlight text %}

<environment>: #development, staging, production
  adapter: makara_mysql2
  encoding: utf8
  reconnect: false
  socket: /var/lib/mysql/mysql.sock
  makara:
    blacklist_duration: 3
    master_ttl: 5
    sticky: true
    connections:
      - role: master
        host: localhost
        pool: 5
        username: <username>
        password: <pwd>
        database: <master_db_name>
      - role: slave
        host: localhost
        pool: 5
        username: <username>
        password: <pwd>
        database: <slave_db_name>

{% endhighlight %}

### Notes -

1. In case any situation where a read has to explicitly go to master, we can either use stick_to_master! method on the model connection OR override the default adapter with a new one. (Ex - <http://www.blrice.net/blog/2014/12/06/scaling-rails-with-distributed-db-reads>)

2. One common scenario where we may need to read from master is immediately after a record's creation. This is just incase replication does not work. So, reload method can be proxied to read from master. But as of now, this can be handled by using sticky option in the config(sticky: true).  Did not find the need to address this during the testing. But, just a word of caution for your app.
