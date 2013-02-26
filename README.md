#Rails


##Creating a Rails project
With the command line, navigate to where you want the project folder to be generated (e.g. documents/my_rails_projects/) and type the following to create a project called project_name: 
     
    rails new project_name

Navigate to that folder and type the following to create a controller called posts:

    rails g controller posts

In text editor, open the file project_name/app/controllers/posts_controller and make sure it says: 

    class PostsController < ApplicationController
      def index
      end
    end

Navigate to project_name/app/views/posts/ and create the file index.html.erb in that folder.
Open project_name/config/routes.rb and under the first row, enter: 

    resources :posts

With the command line tool, make sure you are have navigated to the project folder, then type:

    rails s

In your browser, go to localhost:3000/posts.
To stop the server, hit ctrl-C.

##Generate a controller and action

    rails g controller <controller name> <action>

##Change layout for entire Controller

    class ProductsController < ApplicationController
      layout "inventory"
    end

In the 'layouts' folder under 'views' you can save different layout styles. In the controller you specify which layout will be used. 

##Change layout for Controller ACTION

    class ProductsController < ApplicationController
      def index
        render :layout => 'special_layout'
      end
    end

This is commonly used when ...

##If "undefined method `body' for..."

     rake db:migrate

##If "database ... does not exist":

    rake db:create db:migrate  

##If server doesn't start: Migrate the database

    bundle exec rake db:migrate  

This needs to be written into the command line if development has been been working on the database and the server doesn't start. 

##can't convert Symbol into Integer

restart server

##psych errors. warning: already initialized constant ANY

     bundle exec rails s
     
or

     gem uninstall psych












##Installing bourbon

http://bourbon.io/
Add the following line in your Gemfile:

    gem 'bourbon'

In the command line, enter:

    bundle install

Restart your server ("rails s" in the command line). Then rename application.css to application.css.scss:

in application.css.scss, delete the folliwing line:

    *= require_tree .

Import Bourbon at the beginning of application.css.scss. All additional stylesheets must be imported below Bourbon:

    @import "bourbon";
    (any other imports below)

##Installing Neat

http://neat.bourbon.io/
First: Install Bourbon.
Add the following line in your Gemfile:

    gem 'neat'

In the command line, enter:

    bundle install 

If you run into 'Bundler could not find compatible versions for gem "sass"', then enter:

    bundle update sass

Within your application.css.scss file place the following on top:

    @import "bourbon";
    @import "neat";

##Installing Bootstrap

Simple and quick way is to download the customized css file from the bootstrap site, rename it to bootstrap.css.scss and import it in the application.css.scss file after bourbon and neat:

    @import "bootstrap.css.scss";












#HTML.ERB

##Create a text link
http://guides.rubyonrails.org/routing.html

    <%= link_to 's', terms_path %>

"Terms" is the text shown for the link. The path needs to exist in config/routes.rb
e.g. 

    get 'terms', to: 'welcome#terms' 

for the link to the page "terms" under the folder "welcome".
Restart server after updating the rb file.

##Image as link, declared in the HTML

    <%= link_to root_path, :id => "root" do %>
      <img />
    <% end %>

##Image as link, declared in the SCSS

    <%= link_to('', root_path, class: 'my_image') %>

In the SCSS, use the "my_image" class to add background-image, or other styling.
The '' makes sure no text is used for the link.

##External link

     <%= link_to("http://www.dn.se") do %>
       <img />   
     <% end %>

##Internal link as button

     <%= button_to "This is a link button", root_path, :method => "get", class: 'btn' %>

##Repeat elements

    <% 3.times do %>
      <li></li>
    <% end %>

##Render a partial

    <%= render 'folder/sidebar' %>

When saving partials, make sure their names start with an underscore and have the file type _PARTIAL.html.erb. They should not be called with an underscore though.

     <%= render purchaseable.events, section: purchaseable %>
     
This renders an array of events from the 'events' folder













#Images

##Insert an image with a class

    <%= image_tag('divider_arrow.png', :class => "arrow") %>

##Insert an image using the asset pipeline

    <%= image_tag("foo.png") %>



##Linking Javascript assets

    <%= javascript_include_tag "main", "columns" %>

##Linking Stylesheet assets

    <%= stylesheet_link_tag "main", "columns" %>

#CSS

##CSS Image Assets

    background: image_url("image.png");

##Align fonts of different sizes to same baseline
Use spans to let text resize from the same baseline.

    <div style="height:100px; line-height:100px; background:#EEE;">
      <span style="vertical-align:middle;">test</span>
      <span style="font-size:2em; vertical-align:middle;">test</span>
    </div>

#Fonts

##Fontello

http://fontello.com/

Select files, download them and place the font files in assets/fonts. 
In the HTML, declare the icon:

    <i class="icon-export"></i>
    
In the SCSS, make sure all the file types are called for:

    @font-face {
    font-family: 'fontello';
    src: url('fontello.eot');
    src:url('fontello.eot?#iefix') format('embedded-opentype'),
      url('fontello.svg#icomoon') format('svg'),
      url('fontello.woff') format('woff'),
      url('fontello.ttf') format('truetype');
    }
    
    [class^="icon-"]:before,
    [class*=" icon-"]:before {
    font-family: 'fontello';
    font-style: normal;
    font-weight: normal;
    speak: none;
    display: inline-block;
    }
    
    .icon-export:before { content: '\e715'; } /* '' */

#Forms

##Formtastic

http://rdoc.info/github/justinfrench/formtastic

###Changing a label for an input

    <%= f.input :defaultname, label: 'Not the default name' %>

If 'label:' is not used the label will read whatever the default name is.

###Number of rows for text area

    <%= f.input :textareaname, input_html: {rows: 10} %>

input_html: can be used for other things such as disabling text fields. 


##Simpleform

https://github.com/plataformatec/simple_form

Add class to an input

     <%= f.button :submit, :class => "btn" %>

Textarea

     <%= f.input :lesson, :as => :text, :input_html => { :rows => 2 } %>
