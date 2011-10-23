!SLIDE
# Rails #

!SLIDE bullets transition=scrollLeft
# Rails #

* Home: [rubyonrails.org][rails-home]
* Rails Guides: [guides.rubyonrails.org][rails-guides]
* Railscasts: [railscasts.com][railscasts]

[rails-home]: http://rubyonrails.org
[rails-guides]: http://guides.rubyonrails.org
[railscasts]: http://railscasts.com

!SLIDE commandline incremental
# Installing

    $ gem install rails
    # ...
    Successfully installed rails-3.1.1
    22 gems installed
    # ...

!SLIDE commandline incremental
# Creating application

    $ rails create my-first-app -T

!SLIDE code
# Dependency Management

    @@@ ruby
    # Gemfile

    source 'http://rubygems.org'

    gem 'rails', '3.1.1'
    gem 'sqlite3'
    gem 'jquery-rails'

    # ...

!SLIDE code
# Dependency Management

    @@@ ruby
    # Gemfile
    # ...

    group :assets do
      gem 'sass-rails',   '~> 3.1.4'
      gem 'coffee-rails', '~> 3.1.1'
      gem 'uglifier', '>= 1.0.3'
    end

!SLIDE code
# Dependency Management

    @@@ ruby
    # Gemfile
    # ...

    group :test do
      gem 'rspec'
      gem 'rspec-rails'
    end


