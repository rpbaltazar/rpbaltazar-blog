---
id: 166
title: Postgres indexes concurrently in ActiveRecord
date: 2016-03-03T08:19:05+00:00
author: rpbaltazar
# layout: post
guid: http://balazar.net/random/?p=166
permalink: /2016/03/03/postgres-indexes-concurrently-in-activerecord/
categories:
  - Databases
  - RoR
  - Software development
tags:
  - active record
  - databases
  - performance
  - postgresql
  - ror
  - web
---
Recently I&#8217;ve had to add new indexes to existing tables in a Postgres database, while developing my Rails project.

I&#8217;ve realized that adding those was taking me a long time due to the amount of data in these tables. I was going crazy until I found out this Postgres option. What happens next is incredible&#8230;.

<!--more-->

During the index creation, even though read operations on the table are still allowed, Postgres locks write operations to that table until the index creation is done.
This can become tricky when you have to run such migrations on production.

The desperation lead me to find out about a Postgres option for index creations: `Concurrently`. This option allows creating an index without locking table access for writing operations (insert, update, delete).

In rails, the referred option became available with ActiveRecord 4 and can be used adding the following to your index: `algorithm: :concurrently`. Nevertheless, the ability for creating an index this way comes with an important detail: **the migration can&#8217;t run inside a transaction**

Such detail implies that the migration should be run used in combination with the `disable_ddl_transaction!`.

Because of the described situation is actually highly recommended that you run the index creation in an isolated migration. All the other migrations will run inside its transaction and rollback automatically if something goes wrong.

Finally, an example of such index creation:
`<br />
class AddIndexToDailyReports < ActiveRecord::Migration
  disable_ddl_transaction!
  def change
    add_index :daily_reports, :report_date, algorithm: :concurrently
  end
end
`
