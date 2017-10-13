---
layout: post
title:      "Creating Users with different permissions in Sinatra"
date:       2017-10-13 22:24:03 +0000
permalink:  creating_users_with_different_permissions_in_sinatra
---


For my final Sinatra project, I decided to make a gradebook app where instructors can post and edit grades, and where students can view grades and register for classes. It is a CRUD app, but needed additional validation checks to make sure that students could not edit course data.  

My original structure for the app was to have an Instructor and Student models, but that quickly led to errors. My app used #current_user method to locate either an instructor or student based on the user id stored in the session hash. However, I ran into issues since there were two models that were users, so that meant that there were two users that shared the same id! Here is my original code:
```
def current_user
	Student.find(session[:user_id]) || Instructor.find(session[:user_id])
end 
```
With this code, every time I tried to find the current user, the student with the corresponding id was returned!  What I needed was to have one model for all users then assign them permissions or roles.  

I refactored the code to have User and Role models, so that there would no longer be an issue of two users having the same id but different permissions. Now each user is assigned a role upon creation which gives them permission to view different things in the app. In the User class, I made two instance methods which return true or false depending on the role of the user:
```
def student?
	self.role == Role.find_by(name: “Student”)
end
def instructor? 
	self.role == Role.find_by(name: “Instructor”)
end
```

These two methods are used throughout the controller actions and erb files to determine what content is shown to which users. For example, this much simplified version:
```
get “/courses/:slug/edit’ do
	if current_user.student?
		redirect “/courses”
	if current_user.instructor?
		erb :”courses/edit”
	end
end 
```

To make sure that I have both Role instances created everytime the app is accessed, I created a helper method in the app controller that creates or finds each role. This method is called before the initial index erb is rendered to the viewer. 
```
get ‘/’ do
	create_roles
	erb :index
end

helpers do
	def create_roles
		Role.find_or_create_by(name: “Instructor”)
		Role.find_or_create_by(name: “Student”)
	end
end
```
Overall I think this approach of assigning permissions through a role class is a good solution and way to go about restricting what certain users can view.  Plus, it gives me the ability to create users with different roles/permissions in the future, such as Teaching Assistants, Deans, etc. 

