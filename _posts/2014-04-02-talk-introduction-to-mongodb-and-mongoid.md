---
title: 'Talk: Introduction to Mongodb and Mongoid'
author: Kieran Andrews
layout: post
permalink: /2014/04/talk-introduction-to-mongodb-and-mongoid/
image:
  - 
categories:
  - Uncategorized
---
I did a talk recently at adelaide.rb and I thought I would share my talk notes, slides and code on my blog for you all to see. Click read more to see it all:

[https://github.com/TigerWolf/mongoid_presentation][1]

<!--more-->



**Presentation notes**

So what is it? Its not quite like the relational databases that most of you would be familiar with like Postgres, Mysql and sqllite. Mongodb is a database that does a really good job of storing documents. Its classified as a NoSQL database and ditches the traditional table-like schema and instead uses JSON like structures. It is used by some major websites including: Craigslist, eBay, Foursquare, SourceForge, and The New York Times. Mongo is the most popular NoSQL database.

Why would you use it? Well mongodb was designed to be fast scalable and flexible. This is mostly because it doesn&#8217;t have relationships or a strict schema. It is also really easy to horizontally scale by adding more nodes. By design, a lot of the work and processing is done on the client (mongoid) over the db server. These design decisions all help keep it fast, scalable and flexible.

One of the cool things about Mongo is that the console is a javascript interpreter which would be familiar to a lot of you here today.

I am sure you are keen to see a demo! I will load up the console now and show you around.

*See the git repository for the demo.*

Now that I have shown you the awesomeness of mongodb. Lets check out mongoid, the ruby ORM for mongodb. The philosophy of Mongoid is to provide a familiar API to Ruby developers who have been using ActiveRecord of Data Mapper.

Mongoid community:  
The mongoid community is quite abundant, you can join in at  
It has Solid documentation at http://mongoid.org  
An active irc at #mongoid  
Also a Mailing List http://groups.google.com/group/mongoid

It also hooks into Active Model, so you get all of the rails goodness. I will show you how to use all of these with Mongoid.

validations  
mass assignment  
serialization (like to_json)  
scopes  
callbacks  
timestamps.  
and many more.

Its also framework agnostic and will work with Sinatra or Padrino.

It also works alongside other ORM’s. For example ActiveRecord or DataMapper. You can create relationships between the two and easily model data that is better in a relational database separately. This allows for a lot of flexibility.

Some of the main features of the Mongoid gem are:

Its powerful query language. It will be familiar to ActiveRecord users. Here are some examples for querying a user. There is standard stuff like searching by name and also greater than and less than operators. 

User.where(:name => &#8220;John&#8221;)  
User.all(:age.lt => 24, :age.gt => 18)  
User.where(:title.in => %w(Ms Mrs))

You can also search in sub documents, like the address of a person. 

Person.where(&#8220;addresses.locations.name&#8221; => &#8220;Chicago&#8221;)

You can also set named scopes just like in activerecord:

class User  
scope :active, :status => &#8216;active&#8217;  
scope :over, :lambda { |age| where(:age.gt => age) }  
end

User.where(:name => /^J/).active.over(40)

This makes it easy to clean up code where you use these queries regularly. 

Validation

Mongoid includes ActiveModel::Validations to supply the basic validation as well as a associated and uniqueness validator.

Some examples:

validates_associated :episodes  
validates :episodes, associated: true

Be aware that Mongoid only validates documents in memory.

validates\_length\_of :password, minimum: 8, maximum: 16  
validates :password, length: { minimum: 8, maximum: 16 }

It also has the alternative syntax as you can see in the examples. 

Another awesome feature of mongodb and mongoid is how it handles

Geospacial indexes

Say you had a set of geo locations that you wanted to store you could model them like so.

class Spot  
include Mongoid::Document

field :name, :type => String  
field :latlng, :type => Array

index [[:latlng, Mongo::GEO2D]]  
end

Using this you could then create a location. 

Ruby Spot.create( :name => &#8220;Majoran Distillery&#8221;, :latlng => [34.924349,138.600379] )

Using this location, and having others already stored in your database you can do

Spot.where(:latlng.near => majoran.latlng)  
#=> [“Majoran Distillery”, ”Cibo”, “Westpac” ]

Or also:

Bar.where(:likes.gt => 100).geo_near([ 50, 12 ]).spherical

There are some popular projects out there that use mongodb. Be sure to check out locomotive cms, Shapado a Q&A style site and Graylog2 for sorting server logs.

Application Spotlight:

Now I will show you a demo application that makes use of Mongoid and displays a list of TV shows from a gem that I am currently working on. This is just a rough use case.

The interface is using angular js and calls the sinatra backend to display the list of TV shows.

*See this is the git repository.*

 [1]: https://github.com/TigerWolf/mongoid_presentation "https://github.com/TigerWolf/mongoid_presentation"