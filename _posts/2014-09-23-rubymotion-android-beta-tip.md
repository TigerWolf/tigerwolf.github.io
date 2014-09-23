---
title: RubyMotion Android Beta Tip
author: Kieran Andrews
layout: post
permalink: /2014/09/rubymotion-android-beta-tip/
image:
  - 
categories:
  - Uncategorized
---
I have been trying out the new Android RubyMotion beta and have been trying out the code samples.

One thing I was frustrated about was having to keep putting the NDK and SDK path in the Rakefile. Here is a quick tip to make it easier.

Create a file somewhere like ~/motion/common.rb

`<br />
@app.sdk_path = '/Android/sdk'<br />
@app.ndk_path = '/Android/ndk'<br />
@app.api_version = "19"<br />
# other common configs<br />
`

Inside the Rakefile for each app:

``<br />
$:.unshift("/Library/RubyMotionPre/lib")<br />
require 'motion/project/template/android'</p>
<p>Motion::Project::App.setup do |app|<br />
  # Use `rake config' to see complete project settings.<br />
  app.name = 'Paint'<br />
  @app = app<br />
  require '~/motion/common.rb'<br />
end<br />
``

If you have a better way to do it, post in the comments below.