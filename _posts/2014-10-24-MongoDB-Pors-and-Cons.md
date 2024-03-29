---
layout: post
title: MongoDB Pros and Cons
tags: MongoDB
categories: Database
---

Happy programmer's day!

Source: http://halls-of-valhalla.org/beta/articles/the-pros-and-cons-of-mongodb,45/

<section class="contentBody"><p>A lot of people are making the switch to MongoDB, however many have neglected to (or outright refuse to) weigh the pros and cons of such a decision. As a relatively new and unfamiliar technology, it can have catastrophic effects when attempting to implement in a production system. In light of this, I've attepted to conduct some research on the topic to find out exactly why one should or shouldn't (or under which circumstances one should) use MongoDB in place of a traditional relational database.</p>
<h4>Background Information</h4>
<p>MongoDB is a document-based <a href="http://halls-of-valhalla.org/beta/articles/nosql,41">NoSQL</a> database. Documents are JSON-style data structures composed of field-and-value pairs for example:</p>
<p>{ "name": "mongo", "age": 5 }</p>
<p>MongoDB stores documents on disk in the BSON serialization format. BSON is a binary representation of JSON documents. Additionally MongoDB uses a JavaScript-based shell and supports JavaScript functions for things such as map-reduce.</p>
<p>A document database has many advantages, but before selecting to use one you should verify that your data fits a document model. <font color="red">Documents should be self-contained pieces of data with structure much like a typical document that a person can print on paper.</font> This previous statement is highlighted to emphasize its importance. I find that data which completely fits the document model is actually quite rare.</p>
<p></p><div class="row-fluid seeMoreSection"><div class="span4 seeMoreLinks">
<b>See More</b>
<ul>
<li><a href="/beta/articles/nosql,41/">NoSQL</a></li>
<li><a href="/beta/articles/php-secure-coding-guidelines,39/">PHP Secure Coding Guidelines</a></li>
<li><a href="/beta/articles/translation-of-unhelpful-neo4j-error-messages,46/">Translation of Unhelpful Neo4j Error Messages</a></li>
</ul>
</div><div class="span8">One would likely argue that data such as a forum with users, threads, and posts is definitely more relational data. But many people suggest that articles fit better to a document model. This may sometimes be the case, but what if articles are written by users who each attributes of their own? What if articles can belong to categories which each have some metadata of their own? At what point to we acknowledge that the data is actually relational? This is a pretty difficult question to answer.</div></div><p></p>
<p>Putting aside the question of "is it relational or not" for the time being, I began to research MongoDB and why some businesses begin to use it and why others chose not to. To begin, I found this video to be very interesting and informative for explaining how a document database works, when it makes sense to use one, and when not to use one. It also clearly explains many of the fallbacks when using MongoDB, and the issue that many people attempt to make the switch to MongoDB without analyzing first whether their data fits into a document model.</p>
<div align="center">
<iframe width="560" height="315" src="http://www.youtube.com/embed/OqBAVC9GGeI" frameborder="0" allowfullscreen=""></iframe>
I recommend skipping to 9:15. <a href="http://www.youtube.com/watch?v=OqBAVC9GGeI&amp;t=9m15s" rel="nofollow">Direct link</a></div>
<br/>
<p>After a bit of research to try to find reasons why MongoDB is better than a traditional relational database, and reasons why it is worse, I constructed a pretty good 'pros and cons' list.</p>
<h4>Advantages</h4>
<p><b>Sharding and Load-Balancing:</b></p>
<pre class="quote">Sharding is the process of storing data records across multiple machines and is MongoDB's approach to meeting the demands of data growth. As the size of the data increases, a single machine may not be sufficient to store the data nor provide an acceptable read and write throughput. Sharding solves the problem with horizontal scaling. With sharding, you add more machines to support data growth and the demands of read and write operations.
-From <a href="http://docs.mongodb.org/manual/sharding/" rel="nofollow">MongoDB</a>
</pre>
<p>When you have extremely large amounts of data or you need to distribute your database traffic across multiple machines for load-balancing purposes, MongoDB has heavy advantages over many classic relational databases such as MySQL.</p>
<p><b>Speed</b> <br>
MongoDB queries can be much faster in some cases, especially since your data is typically all in once place and can be retrieved in a single lookup. However, <font color="red">this advantage only exists when your data is truly a document</font>. When your data is essentially emulating a relational model, your code ends up performing many independent queries in order to retrieve a single document and can become much slower than a classic RDBMS.</p>
<p><b>Flexibility</b><br>
MongoDB doesn't require a unified data structure across all objects, so when it is not possible to ensure that your data will all be structured consistently, MongoDB can be much simpler to use than an RDBMS. However, data consistency is a good thing, so when possible you should always attempt to ensure that a unified structure will be applied.</p>
<h4>Disadvantages</h4>
<p><b>No Joins</b><br>
In MongoDB there exists no possibility for joins like in a relational database. This means that when you need this type of functionality, you need to make multiple queries and join the data manually within your code (which can lead to slow, ugly code, and reduced flexibility when the structure changes).</p>
<p><b>Memory Usage</b><br>
MongoDB has the natural tendency to use up more memory because it has to store the key names within each document. This is due to the fact that the data structure is not necessarily consistent amongst the data objects. </p>
<p>Additionally you're stuck with duplicate data since there is no possibility for joins, or slow queries due to the need to perform the join within your code. To solve the problem of duplicate data in Mongo, you can store references to objects (i.e. BSON ids), however if you find yourself doing this it indicates that the data is actually "relational", and perhaps a relational database suits your needs better.</p>
<p><b>Concurrency Issues</b><br>
When you perform a write operation in MongoDB, it creates a lock on the entire database, not just the affected entries, and not just for a particular connection. This lock blocks not only other write operations, but also read operations.</p>
<pre class="quote">MongoDB uses a readers-writer lock that allows concurrent reads access to a database but gives exclusive access to a single write operation.
When a read lock exists, many read operations may use this lock. However, when a write lock exists, a single write operation holds the lock exclusively, and no other read or write operations may share the lock.
Locks are "writer greedy," which means writes have preference over reads. When both a read and write are waiting for a lock, MongoDB grants the lock to the write.
-From <a href="http://docs.mongodb.org/manual/faq/concurrency/#what-type-of-locking-does-mongodb-use" rel="nofollow">MongoDB</a>
</pre>
<p><b>Young Software: Inexperienced User-Base; Still Under Construction; Little Documentation</b><br>
MongoDB is relatively young, particularly compared to relational databases. SQL was released in 1986, so it has been quite extensively tested and documented, and there exists quite a bit of support. MongoDB, however, has only been around since 2009, so most users are not experts and there does not exist such a large base of knowledge available on the web by comparison. </p>
<p>This leads to very common misunderstandings such as the one related to the "safe mode" option.<br>
When safe mode is set to false, writing is basically asynchronous; it is actually just an insertion into a staging document, not an actual database write. The data will only be written to the database at a later time, so you don't have any assurance about data integrity.</p>
<pre class="quote">Often developers don't understand that without safe=True, the data may never get written (e.g. in case of error), or may get written at some later time. We had many problems (such as intermittently failing tests) where developers expected to read back data they had written with safe=False.
-From <a href="http://blog.scrapinghub.com/2013/05/13/mongo-bad-for-scraped-data/" rel="nofollow">ScrapingHub</a>
</pre>
<p>Note that safe=false was the default setting before November, 2012.</p>
<p>The code is still very much under development, so that makes MongoDB an interesting piece of software to play with, but when you're trying to develop a professional project it might not be good to be a beta tester. </p>
<p>For example, before version 2.2, MongoDB did not yet have their aggregation framework, so in order to aggregate data you were stuck using group(). The problem with group() is that can only handle up to 10,000 unique keys, and additionally it returns a single document which means you can't perform any sort of "order by". </p>
<p>Users also often make the mistake of believing that instead of using a database along with some form of caching system, they can just use MongoDB as their database and the cache. This is not what MongoDB was designed for. When you want to put an object into cache use something like Memcached; that's what its purpose is.</p>
<p><b>Transactions</b><br>
MongoDB doesn't automatically treat operations as transactions. In order to ensure data integrity upon create/update you have to manually choose to create a transaction, manually verify it, and then manually commit or rollback.</p>
<pre class="quote">Operations on a single document are always atomic with MongoDB databases; however, operations that involve multiple documents, which are often referred to as "transactions," are not atomic. Since documents can be fairly complex and contain multiple "nested" documents, single-document atomicity provides necessary support for many practical use cases.
Thus, without precautions, success or failure of the database operation cannot be "all or nothing," and without support for multi-document transactions it's possible for an operation to succeed for some operations and fail with others. 
-From <a href="http://docs.mongodb.org/manual/tutorial/perform-two-phase-commits/" rel="nofollow">MongoDB</a>
</pre>
<h4>Conclusion</h4>
<p>It's clear that the cons list is a somewhat longer list here, but that isn't to say that MongoDB should never be used or that it isn't the optimal solution in some cases. It also doesn't mean that MongoDB doesn't have a lot of potential; it is still a very young and immature database which is currently within the beginning of its development phase. </p>
<p>Developers need to be aware that MongoDB is not a replacement for relational databases; it is designed for a specific scenario in which it excels. And the point should also be made that one should definitely not attempt to force a square peg through a circular hole. Don't try to force your data into a particular model just so that you can use a particular database; you will have issues in the future if you try. Don't do things just because they're cool; do them because it makes sense.</p>
<p><b>Sources:</b></p>
<ul class="bbcodeList">
<li><a href="http://docs.mongodb.org" rel="nofollow">MongoDB Documentation</a></li>
<li><a href="http://blog.scrapinghub.com/2013/05/13/mongo-bad-for-scraped-data/" rel="nofollow">Scraping Hub</a></li>
<li>Image from MongoDB.</li>
</ul>
<p></p></section>
