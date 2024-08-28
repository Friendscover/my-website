---
layout: post
author: Tobias Klöpper
---

In my last blog post I was complaining about the lack of support for german banking cards as the default payment for some cloud hosting providers like [render.com](https://render.com) or [heroku](https://www.heroku.com/). After some time off I came back to the same problem. I did some searching around and found out about [Digital Ocean](https://digitalocean.com/). And to my surprise they are providing Paypal as a payment option. There was only one problem. Digital Ocean provides configurable servers instead of the one click deployment solutions by other providers. That should not be hard so set up, right?

### Starting with the lowest tier

Starting off with an initial prepayment of five bucks, my account was ready to host my projects. Initially my goal was to use the cheapest server, because my boardgame_winner Rails app was just a hobbyist project. The server was easy to set up. It was just two clicks and you are done. Connection was done via my terminal over `ssh`. Github uses `ssh` for git updates therefore I was familiar with generating a ssh-key pair to connect to the server. Shortly after I was connected to the server and I was starting to install the relevant packages and rbenv to install the latest ruby version. Everything worked fine, until the ruby install started. The usual install 

{% highlight ruby %}
rbenv install 3.2.2 --verbose 
{% endhighlight %}

failed after 98%. The server ran out of disk space (or RAM, I don`t remember). I tried it a second time but the error message was the same. On the brink of giving up I was looking at other peoples guides to deploy on Digital Ocean. Then I found the Ruby on Rails [one click deployment](https://www.digitalocean.com/community/tutorials/how-to-use-the-ruby-on-rails-1-click-install-on-digitalocean).  

### It is finally working!
For the one click deployment you just need to choose an server image and the corresponding payment plan. And at this point I found out why my manual install failed. For the RoR environment Digital Ocean recommends at least 1 GB of RAM. This is included in the 6€ droplet price tier. My initial 4€ server setup just ran with 500 MB of RAM. In hindsight I should have recognized my initial mistake. But the server is up and running now.

### One final step
The default Rails droplet creates an example Rails App. Therefore I had to ssh into the server and clone my git repository on Github. For the last step there needs to be a new Postgresql DB Table for the corresponding Rails application. In my case I added a `boardgame_winner_development` and `boardgame_winner_test`` table. Finally migrating the DB in Rails and restarting the rails with server systemctl stop rails.service!


### Conclusion
I went over too many obstacles to get my damn project to live deployment. If you are ever in the same situation, just use any other service with a credit card. But for me Digital Ocean seems to be perfectly running and I did not have any problems yet after setting up the deployment. Now it is time to refactor my code and add some automatic deploys.
