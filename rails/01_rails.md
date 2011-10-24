!SLIDE
# Rails #

!SLIDE bullets
# Rails #

* Home: [rubyonrails.org][rails-home]
* Rails Guides: [guides.rubyonrails.org][rails-guides]
* Railscasts: [railscasts.com][railscasts]
* Stack Overflow

[rails-home]: http://rubyonrails.org
[rails-guides]: http://guides.rubyonrails.org
[railscasts]: http://railscasts.com

!SLIDE bullets incremental
# Rails provides:

* MVC separation
* ORM (ActiveRecord)
* RESTful Routing
* DRY views with partials and helpers
* Extensible generators
* Dependency Management with Bundler

!SLIDE
# Model

    @@@ruby
    class Post < ActiveRecord::Base
      has_many :comments

      belongs_to :author, 
        :class_name => 'User',
        :foreign_key => :author_id

      validates :body, :author, 
        :presence => true
    end


!SLIDE
# Named scopes

    @@@ruby
    class Post < ActiveRecord::Base
      scope :last_week, lambda { 
        where("created_at < ?", Time.zone.now) 
      }
    end

!SLIDE
# Querying DB

    @@@ruby
    User.find_by_email("...").posts
      .last_week.includes(:comments)

    post.comments.where(:author_id 
      => post.author_id)


!SLIDE commandline incremental
# Generators

    $ rails generate model Post author_id:integer body:text
        invoke  active_record
        create    db/migrate/20111024214542_create_posts.rb
        create    app/models/post.rb
        invoke  rspec
        create    spec/models/post_spec.rb
    $ rake db:migrate

!SLIDE
# Migration

    @@@ruby
    class CreatePosts < ActiveRecord::Migration
      def change
        create_table :posts do |t|
          t.text   :body
          t.integer  :author_id
          t.timestamps
        end
      end
    end

!SLIDE commandline incremental
# Generators

    $ rails generate controller Posts new
    # creates controller, view, spec, route, 
        posts.js.coffee, posts.css.scss

!SLIDE
# Controller

    @@@ruby
    class PostsController < ApplicationController
      def new
        @post = Post.new
      end

      def create
        @post = Post.new(params[:post])
        if @post.save
          redirect_to @post
        else
          render :new
        end
      end

      # ...
    end

!SLIDE
# Routing

    @@@ruby
    resources :posts

!SLIDE commandline incremental
# Routing

    $ rake routes
        posts GET    /posts(.:format)     {:action=>"index", 
                                           :controller=>"posts"}
              POST   /posts(.:format)     {:action=>"create", 
                                           :controller=>"posts"}
     new_post GET    /posts/new(.:format)      {:action=>"new", :controller=>"posts"}
    edit_post GET    /posts/:id/edit(.:format) {:action=>"edit", :controller=>"posts"}
         post GET    /posts/:id(.:format)      {:action=>"show", :controller=>"posts"}
              PUT    /posts/:id(.:format)      {:action=>"update", :controller=>"posts"}
              DELETE /posts/:id(.:format)      {:action=>"destroy", :controller=>"posts"}

!SLIDE
# View

    @@@html
    <%= form_for @post do %>
      <p>
        <%= f.text_area :body, 
          :size => "60x12" %>
      </p>
      <p>
        <%= f.submit "Create" %>
      </p>
    <% end %>

!SLIDE bullets incremental
# Much more...

* Asset pipeline
* Caching
* Multiple resource formats (XML, JSON, HTML)
* Mailing
* ...

!SLIDE bullets
# Rails alternatives:

* Sinatra
* Padrino
* Rack

!SLIDE bullets
# Sinatra

* [sinatrarb.com][sinatra]

[sinatra]: http://sinatrarb.com

!SLIDE
# Sinatra

    @@@ruby
    require 'sinatra'

    get "/info" do
      %x[redis-cli info]
    end

!SLIDE
# Padrino

* Full-featured framework
* Based on Sinatra
* [padrinorb.com][padrino]

[padrino]: http://padrinorb.com

!SLIDE
# Rack

    @@@ruby
    use Rack::Static, :urls => ["/media"]

    run MyApp
