---
title: My Startup Weekend in Adelaide
author: Kieran Andrews
layout: post
permalink: /2012/12/startup-weekend-adelaide-my-experiences/
image:
  - http://kieranandrews.com.au/wp-content/uploads/2013/09/startup-weekend-172x300.jpeg
categories:
  - Development
  - Ruby
---
I recently attended [startup weekend in Adelaide][1]. I was really excited because it would be a good opportunity to build something and test my new skills I had learn recently [programming ruby][2] (and using rails).

The weekend started on Friday night where attendees had the chance to pitch their ideas in a quick 1 minute pitch. There where some exciting ones. The ones that stood out for me was a pitch about a rating system for health care professionals , a iPhone app to find and rate pubic toilets and a coffee rating app.

I decided to join the team doing rating and listing of health care as I though this would be really useful for lot of people if it was successful and seemed like something I could help and build a great MVP.

On the Saturday, after having formed our team on the Friday night, we where all ready to go. We had a really large group which became quite hard to manage at the start, we decided to break the group up into technology (MVP) and business so we would all.

In creating the initial product and setting up a starting point I made a few mistakes with setting up my project. Something that I found really useful and saved me a lot of trouble, was a ruby gem called [Composer][3]. It gets a project up and running really quickly by asking you a series of questions of things that you might want to add to your project, like [Devise][4] for auth and [Twitter bootstrap][5].

Wanting to get something up and running really quickly, Luke in our group recommended Heroku. I had never used it before but wanted to give it a go. I was really impressed! All you need to go is install the Heroku gem on your computer, run heroku init on the project and then type git push heroku and it is deployed in a matter of minutes! It runs bundle and install all of the gems in the gemfile and then spins up a server.

One of the elements of the weekend that I really enjoyed was the mentors  that came to each group and provided insight into the various aspects of our project and how we could improve. This was really interesting to hear.

I made quite a bit of progress with the app and by the end I was able to make a simple way to lookup a directory of health care professionals. We used the app in our pitch at the end of the weekend. The other pitches where really good to watch and to see what all of the other teams had come up with over the weekend.

 [1]: http://adelaide.startupweekend.org/
 [2]: http://tryruby.org/levels/1/challenges/0
 [3]: https://github.com/RailsApps/rails-composer
 [4]: https://github.com/plataformatec/devise
 [5]: http://twitter.github.com/bootstrap/