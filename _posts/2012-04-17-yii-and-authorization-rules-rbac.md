---
title: Yii and Authorization Rules (RBAC)
author: Kieran Andrews
layout: post
permalink: /2012/04/yii-and-authorization-rules-rbac/
categories:
  - Uncategorized
---
One thing that has recently puzzled me with my discoveries of the Yii PHP framework is to do with how authentication rules work. (In particular RBAC)

I have been recently working on a big project for work that is quite complex with quite a few different systems that are all connected to each other. It also supports different devices, like the iPad and the iPhone. For this app it is important to restrict a user to a particular set of assets (that they create) and share these with other users in their company. To implement this, I stared by looking into the standard approach recommended by Yii documentation and that is the [Authorization Component][1]. On the implementation level, You have the option of either doing rules based on a file ([CPHPAuthManager][2]) or using a database backend ([CDbAuthManager][3]).

After doing a bit of research, using the CPHPAuthManager for a large application is a bad idea. Everything is stored in a file and every time a access rule needs to be evaluated, this file will need to be checked. Also all role assignments are stored here, so if you have a large amount of users then there will be a lot of information stored in this file. This would make it unmanageable and wouldn&#8217;t scale very well for bigger applications.

It appears that CDbAuthManager would be the solution. What it does is store all of your access rules in the database. The auth manager will generate a pre-built database schema that Yii provides. The first thing I found was the component that is available in the Yii repositories called [yii-rights][4]. This extension allows you to manage your Authorization within the app and create access rules as needed. The problem with this is that its all held in the database and I would be deploying this application to the production server after testing it on the staging server and did not want to have to create access rules in both instances and have to update them every time we made any changes to the rules.

This is where we came up with the idea of using a console command to create all of our access rules. Yii has a great system for creating console commands you can run on the server, if you want to learn more, [check this out][5]. This console command creates all of our access rules when run and stored them in the database so that we can version control our access rules and have them in one central place.

The problem I have with out current system is that the access rules have business rules that are evaluations to check the current user against the part of the system they are trying to access or modify. What I dont like is that the access rules are in the database and then eval&#8217;d by php at runtime. Now this is a bad idea and most in the php community would tell you to stay away from eval for most things. The question I have is, is this used well or could it have been done better?

If you have something to share that might shed some light on what I might have missed or another way to do it, post your comments below or post to my question on stackoverflow: http://stackoverflow.com/questions/9597287/what-is-the-reason-for-having-authorization-rules-in-the-database-in-yii-applica

 [1]: http://www.yiiframework.com/doc/guide/1.1/en/topics.auth
 [2]: http://www.yiiframework.com/doc/api/1.1/CPhpAuthManager
 [3]: http://www.yiiframework.com/doc/api/1.1/CDbAuthManager
 [4]: http://www.yiiframework.com/extension/rights/
 [5]: http://www.yiiframework.com/doc/guide/1.1/en/topics.console