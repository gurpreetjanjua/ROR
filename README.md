# README

The first step is to install some dependencies for Ruby and Rails.

> To make sure we have everything necessary for Webpacker support in Rails, we're first going to start by adding the Node.js and Yarn repositories to our system before installing them.

    sudo apt install curl
    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

    sudo apt-get update
    sudo apt-get install git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn

## Install `rbenv`  and then `ruby-build`
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    exec $SHELL

    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
    echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
    exec $SHELL

    rbenv install 2.7.0
    rbenv global 2.7.0
    ruby -v

The last step is to install Bundler

    gem install bundler

## Installing Rails
    gem install rails -v 6.0.2.1

If you're using rbenv, you'll need to run the following command to make the rails executable available:

    rbenv rehash

Now that you've installed Rails, you can run the rails -v command to make sure you have everything installed correctly:

    rails -v
    # Rails 6.0.2.1

## Setting Up MySQL
You can install MySQL server and client from the packages in the Ubuntu repository. As part of the installation process, you'll set the password for the root user. This information will go into your Rails app's `database.yml` file in the future.

    sudo apt-get install mysql-server mysql-client libmysqlclient-dev

Installing the `libmysqlclient-dev` gives you the necessary files to compile the `mysql2` gem which is what Rails will use to connect to MySQL when you setup your Rails app.

## Final Steps
And now for the moment of truth. Let's create your first Rails application:

    #### Create first ror app
    rails new myapp

    #### If you want to use MySQL
    rails new myapp -d mysql

    # Move into the application directory
    cd myapp

    # If you setup MySQL with a username/password, modify the
    # config/database.yml file to contain the username/password that you specified

    # Create the database
    rake db:create

    rails server