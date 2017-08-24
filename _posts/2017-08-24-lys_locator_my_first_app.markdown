---
layout: post
title:  "LYS Locator... my first app!"
date:   2017-08-24 00:44:54 +0000
---


For my first app, i decided to create an app geared towards my hobby of knitting and crocheting! LYS Locator finds local yarn stores near you via a zip code or postal code search, and it can search internationally!

This project was tough to get through compared to the earlier labs and final projects. I started the app at the end of July, but was put on hold for about 3 weeks because of illness, a computer breakdown, and a quick vacation. My forced time away from programming was a blessing in disguise, because I had a chance to read [99 Bottles of OOP](https://www.sandimetz.com/99bottles/), which helped me approach the project through an OOP lens and organize my classes. When starting the app, most of the classes that were needed became obvious to me: Scraper, CLI_Interface, and Store. However I really struggled over whether or not to create a class that represented location. 

When I first started the app (before reading 99 Bottles), I thought it made sense to create a class called Location, since the searches were done by location. On returning to the project I realized that the name Location was not accurate to what the class represented, which was actually a location *search*, since the return of the program was not limited to the zip/postal code you search but also includes stores from the surrounding area. Once I started thinking about this class in terms of a search, I realized that one store can show up in multiple searches (neighboring zip codes) and became worried that there would be multiple instances of store created for the same store. I then thought that I could solve this issue by giving the search class and Store a *has many* relationship. The search class would have many stores and each store would have many search's to which it would be a result of. Upon further reflection, I realized that this relationship doesn't make sense in OOP because it should not be a store's responsibility to know what searches it appears in. 

I ultimately settled on not including the class because it made sense to me for Stores to keep track of the stores in the current search. This is such a simple app that I wanted to keep the code simple, and adding in another class just to store the current search results seemed to needlessly complicate the code. However, if i were to expand on this project in the future and allow users to also search by city, state, and country, then I would add in a class that represents each search to take in the user input and convert it to something that the other classes can use. At that point, I may change over the responsibility of storing the stores from the search to their related instances of the search class. 

I also had some struggles using git. I know I accidentally committed a few times with no changes or included changes in a commit that were outside the scope of the commit message. Woops! I think I got better about both of these issues as I got through the project and will be more careful about this going forward. 
Also creating a gem is really confusing and difficult! I thought I could do it easily, but was never able to get it to properly run on my computer using just `lys-locator`. My files appear to be all correct, but I guess I’m missing something! Though I have not given up and will look into this some more in the future. 

Overall, I am pretty proud of this app! It does exactly what I want it to do, it looks visually pleasing on the user end, and I (think) that it is coded well! Check it out on GitHub and let me know what you think: https://github.com/lpassamano/lys-locator-cli-app
