I created two ubuntu servers 
I installed Jenkins and docker on ubuntu servers. 
Once jenkins is setup, I created pipeline project (mention all github details)
and initiated the built.

First server: 
Uses the code to run the Hello world application container and pushes to dockerhub

Second server:
Pulled the created images from dockerhub. 
I used second server to show that, we can pull the image(which we created, i.e. Hello world) anytime.
