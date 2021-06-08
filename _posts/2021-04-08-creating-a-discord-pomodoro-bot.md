---
layout: post
author: Tobias Klöpper
---

- discord ruby gem
- easy methods mapped to api calls
- fun sideproject before starting my BA thesis

## Pomodoro

A Pomodoro Timer was one of the first projects I did as part of the [TheOdinProjects]() Curriculum in 2019. The timer just uses `Javascript` and some basic `HTML/CSS` to display the time in a fashionable way. Since building the timer myself, I have been using the Pomodoro study method to focus on my studies and to be more productive.

It should still be visitable via [Github pages](https://friendscover.github.io/pomodoro/)

## Helping a friend

A few weeks ago a friend of mine mentioned his problems to stay productive and focus on studying for his upcoming exams. He explained that his time is often spend on games or procrastination. I told him about my usage of the pomodoro technique and he seemed interested in using it himself. At that point I thought about studying together to encourage each other. Wouldn't it be cool, to have a timer bot for each study session?

Then I looked into Discord bots and started to work on one.

## What should the bot do?

- set custom times and count down
- notify each user in the voice chat about the time
- play a sound after finishing a session


## Discord API wrapper

My search did not last that long. After a few minutes, I found a well maintained gem for the Discord API, written in Ruby. This seemed to perfectly match my preferences. Here is a [link to the gem](https://github.com/shardlab/discordrb).

## Saving the bot token

Discord API calls need a token for your application/Bot to work. There are different methods on saving the bot token locally, without exposing it on the Internet. First I used a `config.yaml` file to store my token and `.gitignore` it.

But to deploy it via Heroku, the bot token is stored in an environment variable on the machine. Just calling the bot with 
{% highlight ruby %}
  bot = Discordrb::Bot.new token: ENV['token']
{% endhighlight %}
does the trick.

## Implementing a response

My bot builds on the basic Ping example, which should return an message, after recieving an special message. So I used the `pom` command to respond to a user wanting to start a session. 
{% highlight ruby %}
  bot.message(start_with: 'pom', in: '#bot-channel') do |event| end
{% endhighlight %}

The bot just respons to calls in the #bot-channel to reduce spam.

## The event block
 
Before stripping the pom message for the amount of minutes a user wants to study, the bot checks if the user is currently using a voice channel. That way I don't have to deal with errors if the bot wants to play a sound without knowing in which voice channel to join. 

{% highlight ruby %}
  if channel.nil?
    event.respond 'You have to be connected to a voice channel.'
    event.respond 'Try again after you joined a channel!'
  else
    minutes = event.content.split(/ /)[1].to_i
    ...
  end
{% endhighlight %}

The event block contains every method that I need to make the timer work. The current channel can be called with 

{% highlight ruby %}
  channel = event.user.voice_channel
{% endhighlight %}

and to pm the users in the voice channel, that use the bot I can just iterate over the `channel.users` array.
{% highlight ruby %}
  channel.users.each do |user|
    user.pm("Starting Pomodoro for #{minutes} minutes")
  end
{% endhighlight %}

## Timer loop

My bot set adds the minutes of the pom call to the current time and just checks every minute, if the time is reached. Maybe there is a more efficiennt example of a timer loop, but I just put my ruby loop to sleep for 60 seconds.

{% highlight ruby %}
  pomodoro_time = Time.new + (minutes * 60)
  ...
  until current_time >= pomodoro_time
    sleep(60)
    current_time = Time.new
  end
{% endhighlight %}

## Play a sound!

After the time loop reaches the time set by the user, the bot joins the voice channel and plays a sound. In my case it a doorbell ring!

{% highlight ruby %}
  bot.voice_connect(channel)
  voice_bot = event.voice
  voice_bot.play_file('data/doorbell-1.mp3')
  voice_bot.destroy
{% endhighlight %}

And once again the event block is here to save my time.

## Input validation? I don't need that

In my case, this bot is used in a private Discord server and I did not feel like adding input validation, like starting more than one session. I trust my friends, that they won't abuse this bot. 

## Final thoughts

This was a really fun side project and it was really easy to work with the Discordrb gem. Also the documentation helped a lot. If you wanna improvev this bot feel free to clone my [repo](https://github.com/Friendscover/pomodoro-discord-bot) or build one for yourself. The sky is the limit! Onto my next project. Actually writing my BA thesis...