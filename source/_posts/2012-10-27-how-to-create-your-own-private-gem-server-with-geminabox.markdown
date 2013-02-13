---
layout: post
title: "How to create your own private gem server with geminabox"
date: 2012-10-27 22:13
comments: true
categories: [Rubygems, Gem Server]
---

# Gem In A Box on [Dreamhost](http://www.dreamhost.com/r.cgi?239314)

Check out the repo @ <https://github.com/shukydvir/geminabox-dreamhost>

How to run Gem In A Box on [Dreamhost](http://www.dreamhost.com/r.cgi?239314) shared hosting.

<!-- more -->

## Installation

1. Create a new domain/subdomain in [Dreamhost](http://www.dreamhost.com/r.cgi?239314) control panel for the gem server make sure that you checked the Passenger (Ruby/Python apps only) option. You must also specify the location of the 'public' subdirectory of the Ruby on Rails (or other Rack-compliant) application at the same time which is just public.

2. SSH to your server and cd to the folder of the domain/subdomain.

3. Clone this repo locally or directly to your [Dreamhost](http://www.dreamhost.com/r.cgi?239314) domain/subdomain you wish to have the gem server.

{% codeblock %}
git clone https://github.com/shukydvir/geminabox-dreamhost.git
{% endcodeblock %}

4. Update the config.ru file with your username and password for the basic authentication or comment these lines if you don't wise no authentication at all.

{% codeblock simple Rack::Auth::Basic block lang:ruby %}
use Rack::Auth::Basic do |username, password|
  username = "username"
  password = "password"
end
{% endcodeblock %}

5. if you have cloned localy you need to upload the files to the server (choose which method you want rsync, scp, etc...)

6. run bundle install on the server.

{% codeblock %}
bundle install
{% endcodeblock %}

if that don't work you need to export the path of the gems on your server should be like this:

{% codeblock lang:bash %}
export PATH=~/.gems/bin:/usr/lib/ruby/gems/1.8/bin:$PATH
{% endcodeblock %}

and then run bundle install.

7. you need to restart the passenger in order for the settings to take place.

{% codeblock Bash lang:bash %}
touch tmp/restart.txt
{% endcodeblock %}

will get the job done.

## Usage

if you did other changes in the code you need to restart the passenger by doing

{% codeblock Bash lang:bash %}
touch tmp/restart.txt
{% endcodeblock %}

in order to use this just add this to your Gemfile

{% codeblock GemFile lang:ruby %}
source "http://your.servers.host"
{% endcodeblock %}

or if you setup the basic auth use this

{% codeblock Gemfile lang:ruby %}
source "http://username:password@your.servers.host"
{% endcodeblock %}

and you can access your private gems hosted on your own private gem server on [Dreamhost](http://www.dreamhost.com/r.cgi?239314).

## Resources

1. [Dreamhost](http://www.dreamhost.com/r.cgi?239314) Passenger - <http://wiki.dreamhost.com/Passenger>
2. Gem In A Box - <https://github.com/cwninja/geminabox>
3. Gem In A Box - Http Basic Auth - <https://github.com/cwninja/geminabox/wiki/Http-Basic-Auth>

## Additionl Informaion

You can create a mirror of rubygems.org with this setup just point your data folder to your mirror folder.

you can user the [rubygems-mirror gem](https://github.com/rubygems/rubygems-mirror) to do this easily.

I'll explain how I did that next post so stay tune...

## Signup for [Dreamhost](http://www.dreamhost.com/r.cgi?239314) account.

if you don't have a [Dreamhost](http://www.dreamhost.com/r.cgi?239314) shared hosting account you can create one using the Promo Code below:

1. $30 discount if you pay for 1 year.
2. $50 discount if you pay for 2 years.

**Enjoy**


### Promo Code: "SHUKYDVIR"
