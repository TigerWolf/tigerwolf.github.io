---
title: 'The mystical &#8220;Tableless&#8221; Model for rails'
author: Kieran Andrews
layout: post
permalink: /2013/09/the-mystical-tableless-model-for-rails/
image:
  - 
categories:
  - Uncategorized
---
I had a bright idea for an improvement for the app I am currently working on. I have a Rails model that has only 2 rows in the database and the data is never changed, it has quite a lot of relationships and is used quite extensively. My idea was to remove the database out of the equasion and create a Model that would be entirely self dependent. Here I will show you my methods of maddness:

<pre class="rails">def MyModel



  include ActiveModel::Validations

  include ActiveModel::Conversion

  extend ActiveModel::Naming



  def self.attr_accessor(*vars)

    @attributes ||= []

    @attributes.concat( vars )

    super

  end



  def self.attributes

   @attributes

  end



  def initialize(attributes={})

   attributes &#038;&#038; attributes.each do |name, value|

     send("#{name}=", value) if respond_to? name.to_sym

   end

  end



  def persisted?

    false

  end



  def self.inspect

    "#&lt;#{ self.to_s} #{ self.attributes.collect{ |e| ":#{ e }" }.join(', ') }>"

  end



end

</pre>