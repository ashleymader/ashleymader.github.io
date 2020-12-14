---
layout: post
title:      "The More You Know "
date:       2020-12-14 14:15:08 +0000
permalink:  the_more_you_know
---


# Ideation
As I was fast approaching the end of the Rails section of the curriculum, I realized I needed an idea for my project. This was a lot easier said than done if I'm being honest. There were a lot of things that I wanted to build but at the same time I really wanted to build something useful. I kept asking to myself "if I were to deploy this, would this app fill a void?".  After waffling for about a week, I landed on my final idea, Sorgente. 

# The Name
Before I tell you what the app is, you first need to know why I chose the name. The translation of Sorgente from italian to english yields you the phrase, "The Source". You should also know that the owners of the famous Flatiron building in New York are none other than the [Sorgente Group](https://sorgentegroupofamerica.com/). Fitting right? 

# Let's Talk Details
My idea was simple, a place where Flatiron students can share resources about coding i.e. *The Source*.  Ok, enough with the nerding out on the name, lets talk details! I find myself and others constantly asking for outside resources to deepen our knowlege on topics we are studying. There are also some topics or details that don't stick as well and going to other websites or videos on youtube has been immensely helpful. Sorgente solves that problem. A central location for students to add resources to and other students can review the resource to say how or if they found it helpful. 

Planning out my models and relationships had me held up for a bit in the beginning. I was afraid that if I didn't make it perfect in the beginning that I would make much more work for myself later. While that's true, I foung that I was stuck in what is commonly referred to as *analysis paralysis*. GASP.  After planning, drawing, mapping, uploading and playing in db.diagram.io and others, I decided enough was enough. I wasn't sure it was going to be right, but I needed to start somewhere. 

Once I started coding the momentum kicked in. I worked long days to write, rewrite, refactor and build on my code. It felt so good! I even began to dream about coding and my project...a little weird but I guess that's what your brain does when it's all you are thinking about or working on. 

# Helpful Resources
After getting my project working, I went back and added some gems. [LinkThumbnailer ](https://github.com/gottfrois/link_thumbnailer) being one. This takes in a URL from the user and then fetches the metadata from the site. I liked this much better because it took the onus of giving an accurate title and description of the site away from the user. A neat added benefit is that it also scrapes for images. This gave me my beautiful image link on my resource show page ([seen here](https://drive.google.com/file/d/1pK3CxL_dmf3hxQrAu7wy24GK6w0pMBaH/view?usp=sharing)). I found setting my params for the Resource to be a bit sloppy because of how my create method is curently written. If I were to come back later, which I plan to, I would make the LinkThumbnailer it's own class. Recieve the URL from the user, store the data and then set the Resource params separately. Separation of concerns wasn't at top of mind when I implemented this feature. 

I also found the [Shutup](https://dev.to/andrewmcodes/stopping-a-runaway-rails-server-7mg) gem to be helpful. My rails server liked to become unresposive at times and I grew tired of looking up the correct verbiage and needing 3 steps to kill it. Install this gem and all you do it yell at your teminal, through text of course, "shutup" and it will kill any open servers you have within that work window. Although, now that I think about it, yelling it outloud also feels pretty good! Kidding kidding. 

The part of the project I found to me most taxing for my mind was DRYing my code. It required thinking more meta than just simply stubbing things out to get it working. Deciding when a helper vs partial vs model method was an interesting mind exercise. I definitely learned a lot from it. 

After all was up and running, I went back and installed the [Bullet](https://github.com/flyerhzm/bullet) gem. This check for any inefficiencies in your code. Specifically it '"will watch your queries while you develop your application and notify you when you should add eager loading (N+1 queries), when you're using eager loading that isn't necessary and when you should use counter cache." This was something I've not really paid any attention to before and really watching my console output was a lesson learned. This actually made me realize that sometimes a partial isn't the best way to do things. If you use a partial in a loop it will load that partial as many times as you have resources. Which, is incredibly inefficiant. I found Jenn Hansen's video, found [here](https://youtu.be/M5SkirQYpp0), to be a great guide on how to make your code a little smarter to avoid this. 

After all refactoring was done I added some styling with Bootstrap. This was my first project using outside gems as well as styling so this was a huge undertaking for me. Especially since we haven't covered any of this in the curriculum to this point. 

# Lessons Learned
All in all, this project was a great learning experience. A million **binding.pry**'s later, I have a working Rails app. I'm extremely proud of how it turned out.  I'll definitely be coming back to this project later to build on what I have. 


Feel free to checkout my [repo](https://github.com/ashleymader/Sorgente). I'm open to any and all suggestions/feedback.




