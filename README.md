rails4-release-notes
====================


##### Strong parameters

```ruby
class ZombiesController < ApplicationController
  def show
    @zombie = Zombie.find(zombie_params)
  end

  def new
    @zombie = Zombie.new
  end

  def create
    @zombie = Zombie.new(zombie_params)
    if @zombie.save
      redirect_to @zombie, notice: 'Created.'
    else
      render action: 'new'
    end
  end
  
  def zombie_params
    params.require(:zombie).permit(:name,:most_wanted)
  end
end
```

##### Before Action

```ruby
class PeopleController < ActionController::Base
  before_filter :set_person
  before_filter :ensure_permission
end
```
"filter" made people think it was only for transforming the response

in Rails 4 we have a new made for it: before_action

```ruby
class PeopleController < ActionController::Base
  before_action :set_person
  before_action :ensure_permission
end
```

###### FLASH

Specify flash types

```ruby
class ApplicationController < ActionController::Base
  add_flash_types :grunt
end
```

```ruby
flash[:grunt] = "grrrunt"
```
or
```ruby
redirect_to @user, grunt: "gruuunt"
```

In our view:

```html
<h1><%= grunt %></h1>
```
So, no more flash[:notice] in our erb file. Just use notice.
