---
layout: post
title: "How do Rails error messages work"
description: "An introduction to ActiveRecord validation errors and flash errors"
category: "Rails"
tags: [ruby, rails, web development]
---
{% include JB/setup %}

<h1>What are ActiveRecord Error Messages?</h1>
<p>ActiveRecord error messages inform end users of validation errors. If a user
tries to submit data that fails the <a
href="http://guides.rubyonrails.org/active_record_validations.html">model
validiations</a> then an error message will be generated.</p>

<img src="http://guides.rubyonrails.org/v2.3.11/images/customized_error_messages.png"/>

<p>Rails makes it easy to let users know they need to get their act together!</p>

<h2>How do ActiveRecord Error Messages Work?</h2>
<p> When update is called on a model, ActiveRecord checks the data being
persisted against any validations model validations. If model validations fail,
then the object we attempted to persist will have error messages attached to it
by ActiveRecord. Those error messages can be accessed with the following
syntax:</p> 

<pre>
model_object.errors.full_messages
</pre>

<p>This will provide a set of descriptive error messages. Those error messages 
can be iterated through and displayed:</p>

<b>app/controllers/users_controllers.rb</b>
<pre>
  current_user.update(some_attribute: some_value)
</pre>

<b>app/views/users/edit.html.erb</b>
<pre>
  &lt;% if current_user.errors.any? %&gt;

   &lt;h1&gt;&lt;%= pluralize(current_user.errors.count, ‘Error’) %&gt; 
   &lt;% current_user.errors.full_messages.each do |error| %&gt;&lt;/h1&gt;
     &lt;h2&gt;&lt;%= error %&gt;&lt;/h2&gt;
   &lt;% end %&gt;
  &lt;% end %&gt;
</pre>

<h1>What are Non-ActiveRecord Error Messages?</h1>
<p>Non-ActiveRecord error messages can be rather than using the system supplied
by ActiveRecord. <a href="http://api.rubyonrails.org/classes/ActionDispatch/Flash.html">These are called flash messages.</a></p>


<h2>How do Non-ActiveRecord Error Messages Work?</h2>
<p>When update is called on a model, either true or false is returned. As one
would expect, true indicates a successful update, as where a return value of
false would indicate a failed update. The boolean return value can be used to let us
know if their was a validation failure. </p>

<b>app/controllers/users_controllers.rb</b>
<pre>
  def update
    if current_user.update(user_params)
      flash[:notice] = "Update Successful"
    else
      flash[:notice] = "Update Failed"
    end
    redirect_to "/"
  end
</pre>

<b>app/views/layouts/application.html.erb</b>
<pre>
  <p><%= flash[:error] %><p>
</pre>
