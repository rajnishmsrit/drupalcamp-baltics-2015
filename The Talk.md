# Using Docker to boost your development experience with Drupal

---

SWITCH TO SLIDE #01

---

Hello guys!

My name is Jürgen and I'm from Estonia. I'm a full time Drupal developer at 
Fenomen web agency. I have about three and a half years of experience with 
Drupal professionally, but unfortunately at the same time I don't have any real 
experience sharing my knowledge and opinions publicly to others.

However, I like to believe that the fear to fail in front of an audience 
shouldn't be the dictating factor not to do it, because if the goal is to 
improve their own and other people's work, then it's more sustainable to give 
than receive.

So I feel that it's my responsibility to make my first real contribution to 
Drupal community today by giving this small talk with my good colleague Mait.

Because the subject is quite large and the amount of time that have been given 
to us to perform this presentation is finite and a good developer is supposed 
to never go overtime, we have left no room for any improvisation.

Also bear in mind that most of the statements made in this presentation are 
made from a developer point of view. So if we talk about pros and cons of some 
topic then we mostly address only those properties that matter most to a 
Drupal developer like myself. Mainly because we simply don't have time to 
analyze everything from the outside perspective.

Demos that we have prepared for you to show are in video format, because too 
often we have witnessed the rage of the demogods, whether the network is 
unreliable or a piece of software just decides not to function.

Hi, my Name is Mait and I work for Fenomen web agency as well. I have been 
working with Drupal a little bit more than a year professionally. Also, this is 
my first DrupalCamp, so I'm very delighted that I have given the opportunity to 
be here in front of you, fellow Drupal enthusiasts.

So now that we have your attention and you briefly know who we are and what to 
expect from this presentation, lets talk about Drupal and Docker. How can these 
two technologies work together and why you should care.

---

SWITCH TO SLIDE #02

---

Like most of the presentations out there, we have given a title to this one as 
well, which is "Using Docker to boost your development experience with Drupal".

We have divided this talk into two major parts.

The first part introduces Docker, what exactly is it and how it works. On 
second part we will be discussing how we at Fenomen ended up using Docker and 
what problems it helped us to solve when developing Drupal based projects.

This presentation is primarily meant for beginners in general, but we hope that 
some of you who think that they already know Docker, still might learn 
something new from this talk.

---

SWITCH TO SLIDE #03

---

So what is Docker?

Docker is a piece of technology that allows you, the developer, to wrap your 
application and all of its dependencies that it needs in order to run into a 
standardized package, which you can run virtually in any host.

The only requirement to get your application running in 98% of the time is that 
you also need to have Docker installed on that host.

Because Docker relies heavily on Linux kernel specific features, you can 
currently run Docker natively only on Linux, but there are official and 
unofficial ways how you can run it also reasonably well on non Linux hosts.

Docker also gives you tools so you can share your application with others with 
ease.

That is I think the most simplified high level explanation I could think of how 
I would describe Docker to a Drupal developer that has never used 
Docker before.

There is obviously much more to Docker than I have managed to describe in that 
short description, but we will focus mostly on these aspects of Docker in this 
presentation, since these are the most important features that you should be 
familiar with if you want to boost your development experience with Drupal 
using Docker.

---

SWITCH TO SLIDE #04

---

Docker only runs natively on Linux, however not everyone is using Linux today 
as their primary development environment.

Fortunately, there are multiple options for running Docker on a non Linux 
host.

The most portable and flexible way to use Docker on non Linux hosts is to use 
whole-system virtualization technology. 

My personal favourite is VirtualBox that allows you to create and manage
virtual machines in my opinion very beginner friendly way.

It can run on many different operating systems and supports large number of 
guest operating systems including Linux.

The primary downside using plain VirtualBox or any other hypervisor like that
is that you have to do most of the initial configuration yourself manually.

Provisioning a guest operating system may also be a bit overwhelming for some 
people.

Normally developers are not interested in wasting their time configuring their 
environment, but instead they just want to get their development environment up 
and running as fast as possible so they could start working on the project 
effortlessly.

So just using VirtualBox to run Docker may not work for everybody.

---

SWITCH TO SLIDE #05

---

The other option is to use VirtualBox in combination with Vagrant.

Vagrant has a good support on many mainstream operating systems like Windows, 
Mac and Linux.

I'm sure some of you here already are using Vagrant today, but are probably 
provisioning the guest operating system with the more widely used provisioners 
like classical shell or more advanced configuration management tools like 
Ansible, Puppet etc.

This is a widely used and working setup to get your development environment 
up and running but since this presentation is mostly about Docker we can take 
a step further and provision the guest operating system and manage Docker on 
it with Vagrant as well, since it has an official provisioner created to 
support Docker.

If you are already using Vagrant, then this option is probably best for you.

---

SWITCH TO SLIDE #06

---

The official and recommended way to get started with Docker is to use very 
recently announced tool called Docker Toolbox.

It is so new that I personally have not yet had time to battle test it in 
everyday work. It was announced about three weeks ago.

If any of you are familiar with Boot2Docker, then you should know that Docker 
Toolbox is here to replace it and it is suggested that you migrate as soon as 
possible.

Docker Toolbox basically is a collection of tools to help you get started with 
Docker quickly on non Linux hosts. The end goal of these tools is to provide 
you a similar experience and the same functionality as you would expect when 
using Docker directly on Linux.

Unfortunately an essential tool for having a great development experience with 
Docker called Docker Compose doesn't work on Windows, so I don't 
recommend using Docker Toolbox on Windows just yet, but I'm absolutely sure 
that it will be supported on Windows in the future. Until then I would use 
Vagrant in combination with VirtualBox on Windows.

But if you are a Mac user, then Docker Toolbox should definitely be your first 
choice working with Docker, because the support for Docker and other tools in 
Docker ecosystem on that platform is superb.

---

SWITCH TO SLIDE #07

---

The architecture of Docker in a nutshell, in context of this presentation,
consists of two primary parts, Docker Engine and Docker Client.

Docker Engine is basically a daemon that runs continuously on your machine as a 
service. Docker Client is a command line tool that a developer can use to 
interact with Docker Engine.

Because Docker Engine and Docker Client can speak TCP to communicate with each 
other, these two programs don't have to be running on the same machine, which 
gives you a flexibility to run and manage your Dockerized applications very 
conveniently on remote machines over the network.

This same flexibility allows you to use Docker very seamlessly for example on 
Mac or Windows.

Despite that, that Docker Engine can run only on Linux, you can still run it in 
Linux based virtual machine and since Docker Client doesn't depend on Linux 
kernel specific features like Docker Engine does, there are binaries for Docker 
Client that you can run directly on Mac or Windows.

So when a developer interacts with Docker Engine on Mac or Windows, he still 
has a sense of feel that the host he is using can run Dockerized applications 
natively.

---

SWITCH TO SLIDE #08

---

So what makes Linux so special that Docker Engine can run natively only on that 
operating system at this time?

Well, there are a couple of reasons for that.

Some of you may know that Docker is a containerization technology. In other 
words it means that your Dockerized applications also known as containers are 
running in isolation from other processes on the same machine.

The isolation is done by the host's operating system kernel itself and not by 
some other piece of software like in case for virtual machines where the 
hypervisor is in the role that isolates your guest operating system from the 
rest of the system.

However, not all mainstream operating systems today are supporting 
container-based virtualization also called operating-system-level 
virtualization.

By that I mean Mac and Windows.

So my theory is that since Linux is considered a mainstream operating system in 
the technology world and the Linux kernel does support container-based 
virtualization, then the only logical conclusion is that there were no other 
feasible options available to choose from.

Then you might ask, what about operating systems like FreeBSD and Solaris that 
are also supporting this container-based virtualization concept?

I'm pretty sure that in the future these operating systems will be supported by 
Docker natively, because Docker has been built in a way that it supports 
switching between different execution environments.

Basically you can write an execution driver for Docker Engine for your 
operating system if it has some kind of containerization primitives in place 
that would allow a process to run in a sandboxed environment.

As far as I know there already is an execution driver available for FreeBSD 
that utilizes the Jails mechanism on that platform to isolate processes, 
although it's still considered as an experimental project.

And also Microsoft has started to understand the importance of containerization 
technology by adding containerization primitives to the Windows kernel, which 
currently are only available in the just released Windows Server 2016 Tech 
Preview 3. So expect to be able to use Docker on Windows in the future as well.

---

SWITCH TO SLIDE #09

---

From a developer point of view, the two primary advantages of container-based 
virtualization over whole-system virtualization is the efficiency, how much 
resources your application needs from your hardware to be able to run and the 
speed, how quickly you can start and rebuild your application.

A typical virtual machine is usually a couple of gigabytes in size, it takes  
minutes to start and many more minutes to rebuild it from scratch. The 
overhead you have when running your application in a virtual machine is much 
larger than running it on your host natively.

The amount of virtual machines you can run on an average laptop is relatively 
low. I would say if you try to run more that ten virtual machines on your 
average laptop then you may already start experiencing performance degradation.

For a developer these figures are not that appealing and because of that they 
usually run their development tools directly on their host because it's faster, 
there is no doubt about that.

However, by doing so, they lose some of the flexibility over their development 
environment. The whole point of isolation that virtual machines or containers 
can provide you, is that you can have the same set of tools with different 
configurations and versions seamlessly on the same machine without ever 
conflicting with each other. And this is why some people are still willing to 
use virtual machines to develop their projects, because the benefit they can 
get from isolation outweighs the performance impact that using virtual machines 
have on their system.

These are the exact issues that you can solve by using containers instead of 
virtual machines for development.

So where is the catch you may ask now? Why isn't everybody using containers 
instead of virtual machines?

The primary disadvantage of operating-system-level virtualization in my opinion 
in practice is that you can not run applications in containers that are 
compiled for a different operating system as your host. For example you can not 
run Windows based executables directly in a container if your host operating 
system is Linux. There is no such limitations for virtual machines.

But since most of the third party services that are usually used in along side 
with Drupal are able to run on Linux anyways, so using containers mostly 
wouldn't be a problem for a Drupal developer.

So like every piece of technology in this world is trying to solve a particular 
problem, operating-system-level virtualization also has its place and purpose 
to exist. Unfortunately it's very uncommon to have a technology that solves 
many different problems at once without making any compromises to other parts 
of the system. The same rule applies to containerization technology as well.

---

SWITCH TO SLIDE #10

---

Now that you have a better understanding of some fundamentals that enables 
Docker to do its work, we are going to explain you next some of the internals 
about Docker in more detail.

One of the building blocks of Docker is the concept of image.

A Docker image is a read-only template, which in simply put is a collection of 
files that your application needs in order to run.

For example an image could contain a Linux distribution like Debian with Apache 
and your Drupal project files.

It is very similar conceptually to a tarball, which is a collection of files 
and directories which you can move around as a single unit.

Depending on your application and its dependencies the Docker image can be 
either very small, something around few megabytes, or very large, from a couple 
of gigabytes to infinity in theory.

Docker image can be pushed into a centralized registry where other parties can 
easily pull it to their machine.

There are several companies that are providing public and private registries on 
the internet today. Docker, a company behind the Docker project also provides a 
public registry to everyone to use for free and a private registry for a fee.

The name they have given to that service is called Docker Hub.

I definitely recommend you to use Docker Hub if you need to make your images 
easily accessible to others.

Docker registry is also available as an open source software, so you can set up
a private registry relatively easily on your own server.

Using a registry requires usually access to a network, so in case where your 
machine is not virtually able to communicate with a registry, there is always 
an option to export an image to a file, which you can move around through other 
mediums.

---

SWITCH TO SLIDE #11

---

There are a couple ways how you can build a Docker image. You can build an 
image either by hand or in an automated way.

The problem building an image by hand is that for example if you have already
built an image by executing a series of commands on top of each other and you 
are required to make a change to that image in the future.

For example you may need to update a library that your application is using or 
patch a vulnerability for a third party service.

And lets say several months goes by and the change will not be done by you, but 
by another developer that didn't build this image in the first place. 

This is a very real scenario that could happen to any of you.

He probably don't have any clue how the image was made and what exactly is 
packed into that image, because there is no history nowhere to be found that 
would tell him the exact steps that were executed to build this image.

Of course you can always document them to somewhere, but it would still be hard 
to manage, especially if there are hundreds of commands that were needed to 
perform to build this image.

So in a sense you literally have given him a black box, which is very hard to 
work with. I'm sure even you, the author of the image probably would not 
remember how exactly you built it yourself.

Although in some use cases you may not have a choice and you have to build or 
extend an image manually, nevertheless there is a better way to build a Docker 
image.

Docker is able to build an image by reading instructions from a text file. The 
official term for that is Dockerfile.

We will not be covering the manual process in this presentation, because 
honestly we personally have not had a reason to use it in practice.

---

SWITCH TO SLIDE #12

---

Another important concept in Docker is a container. Without understanding the 
basics of it, it's very hard to understand how Docker works.

From a developer point of view, a container provides an isolated virtual 
environment for your application that feels like a lightweight virtual machine.

But architecturally they still are different virtualization concepts.

This means that your application process is virtually isolated from other 
processes running on the same machine.

From an application point of view, there is a little or no difference when 
running your application inside or outside the container. The inside looks most 
of the time the same like outside.

Sharing the host's operating system kernel with other containers, allows your 
application to be more efficient, but still giving you virtual machine like 
capabilities.

Containers are created from Docker images. 

By giving right capabilities to a container you can even make your physical 
devices available to your application running inside the container.

In same cases for example you may need to debug a service that is running 
inside the container, then Docker is able to give you a shell to a running 
container.

A container can have a separate network interface or share a network interface 
with host's interface or with other containers. You can also control how much 
resources your applications can have on the host. You may want to limit the 
memory, CPU or disk space consumption to a specific value if for example you 
run multiple containers on the same machine.

Because you have such a fine control over resource allocation, Docker also 
gives you tools to get the necessary metrics for your application, which you 
can use to monitor you application performance.

Containers are very lightweight. You could run hundreds, even thousands of 
containers on a single host, that's how lightweight they are when compared to 
virtual machines.

Starting a container takes most of the time only a couple seconds or less. 
Usually the application or service running inside the container takes more time 
to start than the container itself.

---

SWITCH TO SLIDE #13

---

For some of you the concept between a Docker image and a Docker container might 
still be a bit unclear.

I once had to explain this to another Drupal developer that also didn't get the 
concept right away.

So the alternative explanation I gave him helped him to better understand it.

Most of you here are PHP programmers, at some time you probably have acquired 
some knowledge about object-oriented programming.

Try to think about the most basic concept of object-oriented programming 
paradigm where you have a class and an object.

A class is a blueprint, which specifies the structure of data and the behaviour 
of your objects.

The same concept can be applied to the relationship between a Docker image and 
a Docker container.

Docker image in this case is like a class that contains your application code 
and all of its dependencies and you create containers that are derived from 
that Docker image, which then are created or destroyed on demand just like 
objects in PHP. So you can run multiple containers from a single image with 
different arguments to modify your application or container behaviour on 
runtime.

You can share a Docker image with other developers as easily as you can share
a class that have been written to a text file, but you can't share Docker 
containers with conventional tools because they are the running instances of 
that image just like objects.

But just so you know, in the future you actually could send a running container 
from one machine to another by being able to create a full snapshot from a 
container, but this feature is still in an experimental phase.

If today you already can create a snapshot only from the container files then 
in the future the snapshot also will include a memory dump.

---

SWITCH TO SLIDE #14

---

I don't want go into much detail about explaining you everything there is to a 
Dockerfile, because most of that you can easily find on the official Docker 
website.

However, to get some better idea how Docker works we still need to give you 
some basic understanding of it.

If you have been listening then you already know that Dockerfile in a way is a 
blueprint for your Docker image.

It's a simple text file that contains a series of instructions on how to build 
an image.

You might be surprised how simple it actually is to work with a Dockerfile.

If you are familiar with Linux command line interface then you basically 
already know how to write a Dockerfile.

The only key difference between executing a command directly in a terminal and 
in a Dockerfile, is that, a command in a Dockerfile doesn't expect you to 
interact with it during the image building process.

So you have to construct your command that expects an input form a user during 
runtime in a way that all the input that your command needs are directly piped 
to that command in advance or using command line flags to make choices if a 
particular command supports that.

---

SWITCH TO SLIDE #15

---

A good example to illustrate this is installing Apache thought a Debian package
management system. By default if you install a package with apt-get install 
without adding any extra flags you will be prompted to make a choice, either 
you can cancel the operation or continue with the installation process.

But if you would let Docker Engine to execute the same command from a 
Dockerfile, the build process would fail immediately, because it's fully 
automated and doesn't expect any interaction from a user.

By adding -y flag to your apt-get install command, a package will be installed 
without first asking your confirmation.

So if your command line fu is not that great, then by writing Dockerfiles you 
will definitely improve that skill by a lot.

---

SWITCH TO SLIDE #16

---

This is how a simple Dockerfile looks like.

You can build a Docker image from it, that installs Apache on top of Debian 
file system and it replaces the contents of the default index.html file with 
the sentence "Hello, DrupalCamp Baltics 2015!".

As you can see the format of the Dockerfile is very simple.

On the first line you have a simple comment that is there to give you some 
insight about the Dockerfile.

On the second line at the left you have an instruction usually in uppercase, 
like in this case the keyword FROM and to the right you have arguments for that 
instruction.

Every other line in Dockerfile expect the comments are following the same 
pattern.

So let's look into more detail about each instruction in this example.

The second line tells Docker Engine what is the base image that your new image 
will be built upon. In this example it will be the official Debian image, which 
contains the files and directories which Debian itself is made out of.

If a base image doesn't exist on your host at the time of building the image, 
it will be automatically pulled from the Docker Hub.

As you may know everything is a file in Linux, so if you think about that 
concept more closely then maybe it's much easier for you to understand how 
Docker images can work.

I know, it helped me to better understand it.

You can use every other Docker image as your base image. This gives us the 
flexibility to reuse already built images and increase the efficiency of the 
image building process.

Lets say we have two different Drupal projects that are going to use Apache to 
serve files over the web.

And use this exact example as the basis for our new Dockerfiles for each 
project.

One of these projects also has to support HTTPS.

So there are several ways how we could approach this problem and solve it.

We just use this exact example for our project that doesn't need HTTPS support 
and create a Docker image from it.

And for the other project we make a separate copy from this Dockerfile and 
modify it by adding some commands that enables TLS for Apache.

But by doing so, Apache will be installed each time we build an image for our 
projects.

So the more efficient way to do it, is to use this unmodified example as our 
base image for the new image that requires HTTPS support.

In that way the build process is relatively short for the other project, 
because Apache is installed only during when we build the base image.

The fifth line is just there to tell who is the maintainer of the image. This 
metadata will be directly stored on the image and can be queried any time.

On line eight, eleven and fourteen, we see the RUN instruction, which is the 
most common instruction in the Dockerfile. RUN instruction executes a command 
and commits the change to file system back into your image.

If you have not yet noticed then you can see that on line eleven we execute
apt-get install with the -y flag, so the build process wouldn't be interrupted,

Line seventeen informs Docker Engine that the Apache is running inside the
container and is listening on port 80. This is useful if your services running 
in multiple containers need to talk to each other and by exposing a fixed port, 
they can easily discover each other.

The last instruction is the entrypoint for your container. In this example 
Apache will be started in the foreground if you launch the container. As long 
as the resulting process lives, the container will also stay running. If the 
process is killed inside the container, the container will also stop.

Now that we have covered most of the basics there is to Docker that are
important, so you would be able follow the rest of the presentation, we are 
now going to show you a small demo where you can see the Docker image building 
process in action,

---

PLAY DEMO VIDEO #01

---

So there you go, in this little demo we built a Docker image and started
a container.

Inside the container, Apache process were started on port 80.

We also saw, that making HTTP request to a loopback address through the web 
browser, we got the actual response form the web server running inside the 
container with the right payload.

An action that only took about a minute to perform in practice took nearly 
half an hour to explain. So this should give you some idea how powerful it is 
to have a Docker in your development environment toolbox.

---

SWITCH TO SLIDE #17

---

With this little demo we have finished the first part of our presentation.

We will now going to talk about why and how we at Fenomen switched our 
development environments from native LAMP setup to Docker to develop Drupal 
based projects.

Maybe you are right now experiencing the same problems as we did in our 
development workflow before discovering Docker and our experience using and 
deploying Docker within our team would give you some insight how to resolve
them.

---

SWITCH TO SLIDE #18

---

Before deploying Docker to our development environments the setup we had in 
simply put, was not very efficient and scalable when working in a team 
environment.

Our team is relatively small and the amount of projects each our developer has 
to work on or maintain at any given time relative to our team size is quite 
large.

Imagine having to work on more than 5 different projects on a single day. And 
more than half of those aren't even developed by you, so the time you would 
need to put into getting each project up and running on a native LAMP setup 
can be quite large.

By native LAMP setup I mean you have a standard Linux environment and every 
tool or service you would need to use in your development workflow is installed 
directly to your host.

Some projects may also be a couple of years old and getting the right tools to 
work on a newer operating system may also be more complicated than it should 
be.

When we also take into account that some of the issues you need to resolve have
a very easy fix that would take you only about ten to fifteen minutes to 
implement, then the total time you have to invest to resolve a single bug might 
be more than three times higher than the initial estimate due to not having 
a proper system and process in place.

Even more time you would need to waste if the fifteen minute bug requires you 
to set up and configure for example Apache Solr server to fix it, which is not 
that easy do to for everyone.

So a bug that would be normally resolvable by any Drupal developer because the 
nature of the bug itself doesn't require a high level of skill, might 
still be too difficult for a junior developer to fix, because he may lack the 
knowledge and the know-how needed to set up the project on his machine.

Our experience has shown that most who are affected directly by using this 
set up are front-end developers, because if they start to set up a bit more 
complex project by their own, they immediately get stuck. Because the area of 
expertise you need to have to work on your task doesn't belong directly to a 
front-end developer's domain.

As you can see there are many issues using this kind of a set up and processes 
in that work environment. 

---

SWITCH TO SLIDE #19

---

If I'm honest with you, then the real reason why we ended up using Docker 
in our development environment was actually by accident. To get a better idea 
what I mean by that, let me start by telling you a short story.

Last year in October one of our junior developers was working on a project. 

Nothing unusual there.
 
At one moment, the file permissions for a project he was working on were 
incorrect.

He thought he could safely resolve them by himself, because he already had 
performed a similar action a couple of times in the past for different 
projects.

But unfortunately at this time everything didn't go as well as he would have 
planned.

When he realized that his system wasn't working properly anymore after 
attempting to fix the file permissions, he notified a fellow colleague for a 
help.

After some investigation what exactly had happened to his system, we found out 
that the following command you can see on the slide, he had entered to his 
terminal had made his system unusable.

For those who don't know what this command does, it changed every file and 
directory ownership on his machine to www-data.

The command in this case were executed as superuser, which makes it extra 
dangerous.

Services running on his host were not able to properly access files and 
directories anymore.

Because this happened in the middle of the work day, we at first tried to 
recover as much as possible by hand so he could at least continue his work for 
the day.

Reinstalling an operating system and configuring all the tools and services 
that a developer might need would have taken us more time than we initially had 
been given.

But unfortunately the effort we put into trying to recover his system was not 
enough.

So the only choice we had, was to reinstall the operating system, install and 
configure all the tools that he needed in order to be able to continue with his 
work.

We are also using phpfarm on our systems to be able to use multiple PHP 
versions in parallel on a single host.

The issue with phpfarm is that you have to compile PHP and its extensions from 
a source code. Compiling a large project like PHP is quite a tedious task, 
especially if the documentation that should assist you, is not up to date or if 
you are using a different Linux distribution or version that the documentation 
was written for.

So the time that a company had lost from two developers that weren't able to 
write code for the rest of the day, was pretty huge as you would imagine.

If we would had a proper process in place that would have allowed us to build 
and configure everything automatically the impact to the cost would have been 
much smaller.

Learning from this real experience how things shouldn't be done, we started 
thinking about how to solve this problem. How to make our development 
environments more efficient.

We learned that Jürgen had already played with Docker in his free time for some 
time now.

By hearing him out, we came to the conclusion that trying to use Docker to 
make our development environments more efficient could actually work.

So we came up with a plan to divide the process of deploying Docker over time 
to our development environments into two phases.

---

SWITCH TO SLIDE #20

---

In phase one, without first introducing large changes to our development 
workflow, we only concentrated on eliminating the problem we had when something 
would happen to your development machine and it couldn't be recovered easily.

The first thing we did, we moved all the services like Apache, MySQL, PHP 
etc., that were running on a developer machine natively into separate Docker 
containers.

We also had to write an in-house tool that would allow a developer to 
transparently manage these containers similarly like you would manage services 
running on your machine with the init system, because we didn't know any 
existing tool at the time, that could have done the same job.

The key thing here to remember is that every Drupal project shared the same 
Apache, MySQL and PHP container instance.

Because a developer still had to know Docker in too much detail and the goal 
was to minimize it as much as possible, we still had some work to do to achieve 
that.

The most critical part to get right was Drush.

How to use Drush in a relatively comfortable way with containers.

Let me give you an understanding of it what I mean by that.

When a developer wants to use Drush in a containerized environment, he first 
has to go inside the PHP container, because Drush was installed along side 
with PHP service.

Then he had to move to the right directory where Drupal files were mounted and 
execute Drush commands there.

This workflow wasn't that intuitive, because using Drush should really be fast 
and easy.

---

SWITCH TO SLIDE #21

---

To solve that, we have created a simple tool called Crush, it's written in 
Bash. 

However in the future we would like to rewrite it in some other more portable 
language, because the support for Bash on Windows isn't that great 
unfortunately.

You can install Crush directly onto your host and use it exactly like you 
would use native Drush implementation.

Under the hood by executing a Crush command, it first tries to detect if your 
PHP container is running, if it isn't, it will ask you if you want to start 
it.

Then it tries to identify if the directory you where executing your command is 
inside the Drupal directory tree and if so it does some magic and executes the 
right Drush command inside the container.

Crush supports Drupal 6, 7 and 8.

From a developer point of view, most of the time he doesn't even notice that 
Docker is the underlying technology that drives his project when using Crush.

Since you can say that Crush in some sense is a version agnostic wrapper around 
Drush then you can use any version of Drush inside the container.

For example you may have to still support an old Drupal 6 project for whatever 
reason that can only run on PHP 5.2 then the only choice you have is to use 
Drush version 5 or lower.

---

SWITCH TO SLIDE #22

---

The second issue that we had to make better was networking. How to make it 
enough transparent for the ordinary Drupal developer that he could still 
develop his projects without knowing how exactly Docker networking works.

As you may know by default when you link multiple Docker containers together 
they don't share the network interface with each other. It means that every 
containerized service in your stack lives in a separate network.

Which we think, is a good property to have in a long run.

Because if two or more random services wants to use the same port, but they 
each have a separate network, we don't have to be worrying about port 
conflicts.

So it allows your project to scale more easily in a development environment.

Because the first phase was not about introducing Docker to our team, but 
instead have a better way to set up a development environment, we had to come 
up with a solution that could hide this from a developer by default, but still 
not restrict it too much that he couldn't use Docker networking features at 
all.

We found this tool called socat and built it into our PHP Docker image.

It allows you quite easily redirect network traffic between two independent 
channels.

So in our case if the developer wants to communicate from PHP with an external 
service like MySQL that lives in a separate container and belongs to a 
different network, he still can use loopback address to communicate with that 
service. So from a developer point of view everything regarding networking 
feels like all the services are still living in the same network.

You should know that socat is not perfect in all cases, because it runs in user
space and not in kernel space it can introduce a noticeable performance hit to 
your project.

So in case if your Drupal project is using lots of modules that are relying 
heavily on database, like Views, Panel, Organic groups etc, it may run 
significantly slower.

In that case you may want to fallback to using direct IP-address to communicate 
with other containers.

Once these two major issues were resolved we started to deploy Docker based 
development environment to couple of developers machines that were willing to 
try it out and test.

The feedback we had collected from them was very useful and after fixing some 
minor issues we already saw awesome results from using Docker in our work 
environment.

For example if one of the developers found a useful service or tool that could 
improve his daily work, we made an image out of it and by doing that we 
immediately could share it with other developers that were using Docker and it 
worked every where the same way.

Another example is where we had a real opportunity to test it out if we 
actually had improved the time how fast we could set up a development 
environment when a new developer joined with our team.

Instead of preparing the machine for a development a day before his arrival we 
did it at the same day within 45 minutes which also included installing the 
operating system and giving him a small lecture about the environment. Which is 
a tremendous improvement from our previous approach to solve that problem.

---

SWITCH TO SLIDE #23

---

But we didn't stop there and here is where the phase two comes in.

We found a tool called Fig which allows you to specify the configuration of a 
multi-container application in a single YAML file.

Today Fig is deprecated and is replaced with an official tool called Docker 
Compose.

Instead of sharing Apache, MySQL and PHP container instances between all
projects on a developer machine, Docker Compose allowed us to use project 
specific containers. 

This is very useful architectural change primarily for one thing.

If your Drupal project differs from the rest of your projects in regard which 
services it needs in order to be able to run, which in practice it usually 
differs a lot, then in a shared environment it's very hard to maintain the 
difference between your services that are running your projects.

For example, your project might need a Redis support from PHP, if you are 
sharing a PHP container with all your projects, then all your projects will 
also have a support for that version of Redis, but what if another project 
needs an older version of Redis or whatever other service or tool in order to 
work. 

So managing a shared system where in practice you absolutely need to have a 
system in place to use project specific containers, becomes extremely hard.

Removing the shared system all together and using an architecture where you 
only have project specific containers running on your machine, with Docker 
Compose is very easy to achieve.

But to make that system efficient you need to have some services and tools in 
place to support it.

Since you could have hundreds of containers running simultaneously on your 
development environment you need a way how to directly access them without 
wasting much time searching for them.

---

SWITCH TO SLIDE #24

---

So we have developed a tool called vhost that itself runs inside a container. 

The purpose of this tool is to listen for events that are emitted by the Docker 
Engine and based on that it displays all your running containers on a single 
web page. So in a sense you can call it the front page of your development 
machine that you can access with your web browser on port 80 or 443. 

Under the hood inside the container runs Nginx that dynamically generates its 
configuration from the events that are emitted by the Docker Engine. So if a 
container dies it will be removed from the Nginx configuration and if a new 
container is launched a new entry will be added to the configuration.

So by using this tool all your multi-container Drupal projects running your 
machine are accessible through DNS. 

Currently vhost doesn't provide DNS service itself.

At fenomen we are relying on an external service, that does DNS for our 
development machines. But one of our goals is to find a way how to do it 
properly on a local machine, so we don't have to rely on an external service to 
do DNS.

---

SWITCH TO SLIDE #25

---

Another essential tool we have developed to have a good experience working with 
Drupal using Docker is called Drupal Compose.






So the next logical step was to create a general purpose docker-compose.yml 
file for Drupal 6, 7 and 8 which covers 90% of Drupal project requirements.

Every dockerized Drupal project should have this file, it's the initial developer 
responsibility to make sure that this file exists on every project. 

To make this requirement easier to manage, I've created a simple shell script 
that generates this general purpose docker-compose.yml file automatically and 
the name for this script is Drupal Compose.

And if the standard docker-compose.yml file is not sufficient enough then it's 
every developer responsibility to make a change to it if he has done some changes 
to environment (creating new Docker images, or setting other parameters for the 
general images etc).

So now that we have a system and a process in place which allows us to define 
project specific environment configurations for our projects, then again no 
matter what is your skill level, you can start working on every Drupal project 
immediately, and you don't have to know the details how some services work for this project.

***cordova sass/less reference

***So we started solving one issue that could have been sovled without Docker as well, 
but by using Docker to solve that we made some great imrpovements in other fields as well.

## Backlog

docker registry phase 2

You should always include third party libraries etc to your Docker project

Presentation link at the start of the presentation


Conclusion - don't take this mission by your own, it will be very hard, try to 
involve your organization into as well so they can support you from the high level, 
but in the end it's worth it because if everyone is doing they work properly 
then your work is also easter due that. Tools like Docker allow everyone to do 
they work better.

old habits - native sass vs docker sass, how to overcome

dynamic runtime -  dockerfile vs puppet etc

thank you at the end and start

## Questions and answers

Make sure to write down any unanswered questions and get back to the questioner as soon as you have the answer. Don't forget to ask them contact details!