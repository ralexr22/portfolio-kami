---
layout: post
title: Blocitoff
thumbnail-path: "img/blocitoff.png"
short-description: Build a self-destructing to-do list application.

---

{:.center}
![]({{ site.baseurl }}/img/blocitoff.png)

## Explanation

To-do lists have become forgotten notes for most people, items that you want to take care of, but with no sense of urgency attached to them. More often than not the information just sits there until you delete it.

Blocitoff will automatically delete items if they aren't completed within 7 days. It will let our to-do list stay clean and free of clutter.

## Problem

I needed a simple page with a clear UI. As long as the site can keep track of items, and update their status, there didn't need to be many more gimmicks. I aimed to make the lists private to users, so we will sign up for a free account with a user name, a password, and an email address. Through the profile page, the user will be able to create multiple to-do lists, each will keep a tally of how old the items on the list are. Once an item is done it can be marked as completed so it can be deleted. The rest of the items will be deleted after a week.


## Solution

The app was styled with [Bootstrap](http://getbootstrap.com/), and I used [Device](https://github.com/plataformatec/devise) to authenticate users. Only one profile per email address would be needed.

When an item is completed, we want to be able to mark it as done and have it come off our list.

{% highlight ruby %}
$("#item-<%=@item.id%>").hide();
{% endhighlight %}

By taking advantage of Rake, I was able to automate the deletion of items that were created 7 days prior.

{% highlight ruby %}
namespace :todo do
  desc "delete items older than seven days"
  task delete_items: :environment do
    Item.where("created_at <= ?", Time.now - 7.days).destroy_all
  end
end
{% endhighlight %}

## Results

With basic controllers and models, like this controller for user:

{% highlight ruby %}
class UsersController < ApplicationController
  def show
    user_id = params[:id] || current_user.id
    @user = User.find(user_id)

    # if the @user is not the current user, redirect to welcome page.
    if current_user != @user
      flash[:notice] = "This list is private"
      redirect_to welcome_index_path

    end

    @item = Item.new
    @items = @user.items
  end
end
{% endhighlight %}

It just took a few lines of code to make a landing page where a user could sign in, or sign up for their own account. Once logged in they could add as many items as they wanted to their list. For the purpose of testing, I seeded data with [Faker](https://github.com/stympy/faker). Finally, I used [Rake](http://guides.rubyonrails.org/command_line.html#rake) to automate the deletion of expired tasks.

## Conclusion

What I created was a clean, simple interface that looks good on any screen size, with features that work predictably, every time.
