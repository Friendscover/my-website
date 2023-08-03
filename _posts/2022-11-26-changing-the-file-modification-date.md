---
layout: post
author: Tobias Klöpper
---
Yesterday I scrolled lazily through my phone and I was looking at the pictures gallery app. Usually the pictures are sorted by their creation date. But there are some pictures with a date, that matches the time I bought a new phone in 2021. Because of manually copying over the pictures their original creation time was reset. This annoyed me so much yesterday that I got to work on resetting their original date.

### First Steps
Most of the pictures were taken by my phone camera or were sent to me via a messenger app. Since their filename matches their creation time, this should not be a difficult tasks to write a little program for resetting the creation time. The fileformat was either  `IMG-20201212-Time`  or  `20201212-Time`. Therefore the creation time was easy to parse as a Date.

### Looking at Powershell
My pictures are stored on Windows, so I first looked into Powershell. After a quick google search, I stumbled upon a [guide](https://abdus.dev/posts/powershell-file-metadata-guide/) to set the creation time via a simple Powershell script.

{% highlight powershell %}
Get-ChildItem | ForEach-Object { $_.CreationTime = "2022-07-17" }
{% endhighlight %}

One step done but the creation data had to be stripped from the filenname. Since I do not know much about Powershell, I turned to my good old friend: Ruby. 

### Working with Files in Ruby
Looking at the docs for the file object in Ruby was my first idea. There I found not only the methods I needed to get the file entries in the current folder but also the `File.utime` method. This method sets the modification time and file changed time to whatever date value you parse as an parameter. [RubyDocs/File](https://ruby-doc.org/core-2.5.0/File.html)

### Stripping the Filename 
At last the filename was stripped via the rubys built in method `String.split`. Including the splitting parameter `"_"` got me the date. Now I need to parse this date through the `Time.parse(date)` function and insert this value as a parameter to the `File.utime` function. Et viola! My pictures now include the correct date. 

### Sourcecode
{% highlight ruby %}
require 'time'

files = Dir.entries(".")

files.each do |name|
    # skip unix parent directories
    next if name.length < 8

    ### save filename
    filename = name

    # strip filename for date
    name = name.split("_")
    date = name[0]

    #resetting file creation date
    date = Time.parse(date)
    File.utime(date, date, filename)
end
{% endhighlight  %}