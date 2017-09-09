# What is a RDS

I must say, the RDS section of AWS is the only happy place there is in their whole offering. This section is the most automated of them all, and I almost fully live up to the dream of, click… click and it just dose stuff automatically. But lets start from the beginning.

RDS is the section where you create and manage all your databases. You have a selection of different provider that you can choose from, and shockingly it is very easy to create a server that will automatically switch to a copy if the main one fails. I know… right?!

# Lets take a step back

Similar to the whole AWS infrastructure, you get a set of legos, and it is up to you to put them together in a way that will make your data resilient and safe.

# AZ Setup

As from what you learned form the other sections, the Availability Zone is a Subnet in your VPC, which physically separate your server from each other. Knowing this, there is a feature when you create a server where you can specify that you want to create the new DB with AZ support (mmm acronyms). This option will create actually two databases (you’ll pay for both) in two different AZ but under the same Region.

Now. Let say that the database that is on a AZ will go down for whatever reason, AWS will automatically promote the other DB that is on the other subnet as the main one, and business will move as usual. Of course the switch will take up to 30 seconds, so during that time your app might not work, but other then that. Everything will just happen automatically. And if the fallen DB will come back on-line it will become the backup one.

Amazing right? It is so nice to see what was promised to us to actually work.

# Backups

So we know how to make your data constantly accessible, but how about backing it up to protect ourselves from a catastrophe? Well you can configure the DB to take a snapshot every single day without taking the database server down, which is actually quite nice.

But what if you wanted to backup the data to the second? Actually this is also easy - I know right, easy, what? I’m serious? Quite serious.

Amazon has this thing called Read Replica. It is basically a regular database that you can only read from. It is normally used in situations where you have a lot of traffic to your site and the majority of the queries that you have to the DB are just read only anyway.

In this situation, you still insert, update and delete from the main DB, but you actually read data from the Read Replica. Even better you can have Read Replicas around the globe with literary one click - I… know right…

What happens in the back is that very time you alter the main DB, it will send an event to all the RR that are connected to it, thus they constable receive in real time all the changes (by the way there is a lag, we are not dealign with quantum entanglement yet).

# Promoting a Read Replica

Since the RR is just a regular DD, it can be promoted to be fully fledged DB with a click of a button. This means that if everything fails in the main DB, you can promote the Read Replica to become a regular DB and switch to it. Thus you lose virtually no data. Just a few minutes of down time.

And this is RDS, it just works as advertised - sadly this is only the exception that proves the rule.