---
layout: post
title:      "All Aboard the Rails Train!"
date:       2017-12-13 02:50:36 +0000
permalink:  all_aboard_the_rails_train
---


Rails and I had a rough start, but after I got used to all of the "Rails magic" I really started to appreciate it and enjoy working in the framework! I had a TON of fun and frustration working on my first Rails app and learned a bunch of new things along the way. My app is **Scavenger Hunt**, it allows users to create scavenger hunts, create teams to participate in hunts, and work cooperatively in teams to find the items in the scavenger hunt! The most challenging part of this project was accounting for the different states of a hunt: pending, active, and completed and what different users are allowed to during these times. For instance the user that created a hunt, aka its owner, can only edit it while it is pending, before its start time, and users who are participating in the hunt can only mark off items as found for their team when the hunt is active, after the hunt's start time but before its finish time. Because of these complexities I focused on the back-end of the app and did very little (ok... basically zero) styling. However I do plan to revist this app in the future and make it look nicer!

Now that I'm done gushing, onto the code!

### Creating a multi-functional helper method

While I was refactoring my views with helper methods, I realized that I was creating multiple helper methods to create an li for a hunt, with only small differences as to what was being displayed. One method displayed the hunt name and date, the other displayed the hunt name, date, and the team of the current user. These methods did not seem very DRY to me, but luckily I remembered that I had read something in The Well-Grounded Rubyist about required vs. optional arguments. This led me down a path to refactor my two original methods into three, which I guess is technically more code, but bear with me through this. 

My original code looked something like: 

```
def li_for_hunt_with_date(hunt)
  content_tag :li do
	  link_to(hunt.name, hunt_path(hunt)) + " | #{hunt.date}"
	end
end

def li_for_hunt_with_date_and_team(hunt, team)
  if current_user.teams.include?(team)
	  content_tag :li do 
		  link_to(hunt.name, hunt_path(hunt)) + " | #{hunt.date}" + tag(:br) + link_to(team.name, hunt_team_path(hunt, team))
	else
	  li_for_hunt_with_date(hunt)
	end
end
```

As it stood, this code was very repetitive, only adding the addition of a link with the current user's team on one branch of an if statement. 

Using what I had recently read about optional statements, I wondered if I could create one method to do the work of both of the above methods. I wanted to create a method that would take in an argument of an instance of hunt and an optional instance of a team.  Here was my next stage in the refactoring process, combining the two methods into one:

```
def li_for_hunt(hunt, *args)
  html = capture do
	  concat link_to(hunt.name, hunt_path(hunt))
		concat " | #{hunt.date}"
		if !team.nil? && current_user.teams.include?(team)
		  concat tag(:br)
			concat link_to(team.name, hunt_team_path(hunt, team))
	 end
 end
 content_tag(:li, html)
end 
```

While this method is technically more DRY, I felt it was overly complicated, was doing too many things in one method, and whether or not it displayed properly hinged on whether or not the coder remembered that you needed to include the optional argument of team in order to display it. I also didn't like that the method name `li_for_hunt` did not clearly state what it would be displaying. My next step in refactoring was to utilize #send, which I had also recently reviewed while reading The Well-Grounded Rubyist. 

```
def li_for_hunt(with_details, hunt, *opt_details)
  content_tag(:li, send(with_details, hunt, *opt_details))
end

def with_date(hunt)
  link_to(hunt.name, hunt_path(hunt)) + " | #{hunt.date}"
end

def with_date_and_team(hunt, team)
  if current_user.teams.include?(team)
	  user_team = link_to(team.name, hunt_team_path(hunt, team))
	else 
	  user_team = ""
	end
	with_date(hunt) + tag(:br) + user_team
end
```

With these new methods, when I call the method to create an li for a hunt it looks like: `li_for_hunt(:with_date, hunt)` or `li_for_hunt(:with_date_and_team, hunt, team)`. Even though it is more code, I felt that this broke down that one larger method into smaller methods with each method having a specific task. I liked that the format of #li_for_hunt now reflects the format of other built in Rails helper methods. 

Even though I ended up with one more line of code than the original two methods, and three more than the refactor down to one method, I feel like this was a good way to tackle the issue I was having with repetition since it broke down the creation of an li into two distinct parts, creating the content and wrapping the content in an li. This allowed me to refactor out repetition in the methods that create the content, which makes it very clear in the two content generator methods that much of the content is repeated by calling one method in the other. Overall, I think the resulting three methods are more readable and concise, but let me know what you think! Check out the [repo on GitHub](https://github.com/lpassamano/scavenger_hunt), or [hit me up on Twitter](https://twitter.com/leighmakesstuff). 

