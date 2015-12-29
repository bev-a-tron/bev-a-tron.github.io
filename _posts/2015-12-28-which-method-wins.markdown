---
layout: post
title:  "Which method wins? (A quick study of Ruby inheritance and include)"
date:   2015-12-28 12:34:56
categories: work
---

I started a new job, and I'm learning Ruby.  I spent some time noodling around with includes and modules and things like that.  I thought I would share my findings.

Then, I realized this hierarchy is written down in "The Ruby Way".  Basically, when you invoke a method, Ruby goes looking in this order:

1. Singletons
2. Methods in the class (this includes included ones)
3. Methods in ancestors (the order matters here)

Hm, no singletons in my example here, but hey, I'm a busy lady.  Hope this helps somebody, even if only my future self.

Code here: [https://github.com/bev-a-tron/ruby_sandbox](https://github.com/bev-a-tron/ruby_sandbox).

~~~~~~~~
module MyModule
  def method_1
    puts 'Inside the module!'
  end
end

class IncludeStuff
  include MyModule
  def method_1
    puts 'Inside include stuff!'
  end
end

x = IncludeStuff.new
x.method_1  # Inside include stuff!

#########################################################


class BaseClass
  def method_1
    puts 'Inside the base class!'
  end
end


class NewStuff < BaseClass
  include MyModule
end

x = NewStuff.new
x.method_1  # Inside the module!


#########################################################


class NewNewStuff < BaseClass
  include MyModule

  def method_1
    puts 'inside the new new stuff class!'
  end
end

x = NewNewStuff.new
x.method_1  # Inside the new new stuff class!

~~~~~~~~

![Signature]({{site.url}}/assets/clear_whale.png)
