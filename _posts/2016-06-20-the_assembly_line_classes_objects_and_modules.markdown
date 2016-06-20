---
layout: post
title:  "The assembly line: classes, objects, and modules"
date:   2016-06-20 23:35:44 +0000
---


I'm a big fan of the assembly line. It changed industries forever. When I was figuring out how to grasp the concepts of classes, objects, and modules the first thing that came to mind was Henry Ford's famous assembly line innovation.

Factories produce the same product repitively very much like how programs and applications perform the same functions. An accounting program will crunch number over and over again through out it's life time. When you start your journey in Object Oriented Programming you begin to learn about classes, objects, instances, modules, super classes, so on and so forth. I want to give my best attempt at helping you (as a newbie to OOR) grasp these concepts based on the 100+ year old assembly line example. 

So here goes nothing...

You manage a factory that provides people with transportation vehicles (for our sake not just for land but for any transportation). The factory manufactures three products: cars, boats, and airplanes. Each of these products are produced on three seperate assembly lines running parallel to each other. Along the assembly lines are machines that assemble together the final product. Business is booming and everyday hundreds of new cars, boats, and airplanes are created. Your assembly line is efficient and can produce mass quantities because it knows exactly what to do- it's been setup that way. In essence the assembly line is the blueprint for the final product. Although every car, boat, and airplane goes down one of the assembly lines, each assmebly has its own set of machines to create the final product. Very much like methods in programming, these machines bring the product to life by building it's characteristics, functions, behaviours like color, velocity, and much more. In Object Oriented Ruby assmebly lines can be comparable to your Classes, the machines can be compared to your methods, and a single new car, boat, or plane is an instance of your assembly line. Same functions, behaviours, charactersitics, but unique.  So, let's get our hands dirty...

![Imgur](http://i.imgur.com/61rAn9N.png?1)

The first thing I did was give the car a *VIN* which is a plain old Vehicle Identification Number. As you can see this is a very simple version of what a car can do. Every car object created through the class will be able to perform these exact functions, but will have it's own VIN. When you create a new object that object will have a unique object_id number. This number makes every instance of a class unique. 

Here is a boat example...

![Imgur](http://i.imgur.com/r0sW3n1.png?2)



When a boat comes off the assembly line as a finished product it followed the exact same blueprint that created all boats before and will create all boats after it. The boat will accelerate. The boat will decelarate. The boat will come to a stop when commanded. All boats share these functions. In the world of programming a new boat would be an object instance of the Boat class.

Here is the plane example...

![Imgur](http://i.imgur.com/5HKK1R8.png?1)


So, let's move on to modules. Let's say the factory owner comes to you and says, "We need to increase our bottom line. We can either lay off workers or come up with a solution that will cut costs". You don't want to lay people off. It sucks. So you start thinking about how you could save the factory money without jeapordaizing people's jobs. Light bulb moment! The machines that create the car, boat, and the plane are very expensive. You realize that all three of these products share 3 exact same functions- you have 9 machines doing the same job!! *EEEEEEEEEK!* Now remember, machines are your methods. So in the car, boat, and plane class there are 3 methods that do the exact same thing.

To solve this problem you sell 6 (leaving you with 3) of the machines and allocate the same jobs to the 3 that's left. In Ruby you can essentially create modules that will save you time and make your program faster. 

Creating a module using the car, plane, boat example. Our module will be called *Move* because those are the characterisitics that are shared by all 3 classes. So, this is a very basic version of what a module would look like...

![Imgur](http://i.imgur.com/9LsbcEu.png?1)

So how do we apply this to our classes (or assembly lines)?

Simple...

![Imgur](http://i.imgur.com/W1im5Kj.png)

As you can see we didin't have to put the functions that were created in the module. We simply took the module and plugged it into the Boat class reducing our work. We would do the same for the car and the plane class as well.

That's it! There is a lot more to classes, instances, objects, and modules but I hope this will help you understand the concept a little better.






