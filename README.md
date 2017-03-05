# Sample Flask App

Thanks for using the Sample Flask App! This application is provided as an example for users who want to create a web application or visualization tool using Python's Flask framework.  It should provide you with all of the pieces necessary to create your own application, including templates for visualization using D3 and Highcharts, a MySQL connection for loading dynamic data, and authentication.  You can use this application in part or in whole to experiment with building your own web applications -- pick and choose the parts you need and go from there.

## Using this README

This README provides summary information about the various modules included in the SFA, including pointers to additional resources.  However, you will find that the code is well commented -- **for in-depth information about the code itself and what it's doing, we recommend that you consult the source code**.

## About Flask
Flask is a popular, lightweight framework for building web applications in Python.  Sometimes considered a "microframework," Flask allows you to pick and choose what you need and leave out anything you don't.  For more information about Flask, the [Flask website](http://flask.pocoo.org/) is an excellent source of information.  We would also point you to the [Flask Tutorial](http://flask.pocoo.org/docs/0.10/tutorial/) if you'd like a hands-on approach to learning Flask. We also recommend the excellent [Explore Flask](https://exploreflask.com) tutorial and use many structural ideas from it.

## Quickstart

### Dependencies

It's recommended that you use a virtual environment when running your app.  You can easily manage virtual environments with [virtualenv](https://virtualenv.readthedocs.org/en/latest/).  To set up a virtual environment in the app, navigate to the app route:
`cd path/to/app`
and run the following command (assuming virtualenv is installed):
`virtualenv venv`
To activate your virtual environment, run 
`. venv/bin/activate`
To deactivate, simply use 
`deactivate`.

Within this virtualenv, you can install dependencies with pip.  An easy way to do this and cover all of the dependencies you'll need is to install from the requirements.txt file:

`pip install -r requirements.txt`

Note that you may need to install several binaries -- notably, a mysql client and an LDAP client, if you don't already have them installed.  You can make pretty good progress against these goals by aggressive Googling of any errors you receive.  Awkwardly, asking the original developers about them is not the best way to go forward, since once you've done this once you pretty much never have to do it again; in other words, we've forgotten how we did it originally :-)

### Credentials

We use an `instance` folder to manage credentials. Remove the `sample-` from the `sample-config.py` and `sample-credentials.py` files in the `instance `app/instance` folder (or copy them) to start.

### Running the app

To run the app in dev mode, make sure the `app.run` line in server.py reads `app.run(debug=True)`.  Then, simply run

`python server.py`

or even 

`./server.py` 

and your app will be available on localhost:5000.

## Credentials

We have passwords and other sensitive variables in our apps. To make sure only you and your co-developers have access, and that it stays out of version control, create a new folder called `instance` in the root directory. We currently have 3 files:

- `__init__.py` - Exposes the `instance` folder to your app 

- `config.py` - Used to set Flask variables like SECRET_KEY for sessions; see the [Flask documentation](http://flask.pocoo.org/docs/0.10/quickstart/#sessions) for more information on SECRET_KEY.

- `credentials.py` - Stores passwords and any other sensitive info. To connect to MySQL, this should include a dict called `mysql` with `host`, `user`, `password`, and `db` keys.

You can copy an example of our `instance` folder in the `resources/` folder in the root directory.

## Environments

### Development

Run your app with `app.run(debug=True)` in `server.py`

### Production

Run your app with `app.run(host='0.0.0.0')` in `server.py`

## Components

Modules are generally located within the `app` folder.  Again, for detailed information, consult the code itself, but here we provide a brief overview of what you can find therein.

### Routes

App routes (i.e., what you get when you go to a certain endpoint within the app -- e.g., "/" or "/foo/bar") are defined within views.py

App routes are decorated with the `@app.route()` decorator.

### User Authentication

Login and logout are accomplished with LDAP.  To do this, we have an LDAP service and a user service in the services/ folder.  Together, these manage our authentication and session information, with the LDAP servicemanaging authentication against the LinkedIn LDAP server, while the user service manages the session information, like logging in and out and finding out who the current user is.

Additionally, we define a `@login_required` decorator signifying whether a certain route requires login.  You can add this to a route under the `@app.route()` decorator to require users to be logged in when they access the route.  If they are not, they are redirected to the login page.  

## MySQL Database

SFA uses a MySQL server set up on a remote database as the primary data service.  You can mimic this database on your own MySQL setup and point the app there by changing the config file.

### Install and start MySQL (OSX only)
1. `brew install mysql`
2. `mysql.server start`

### Set up a new db and user
1. `mysql -u root`
2. `create database sfa;`
3. `create user 'sfa'@'%' identified by 'password';`
4. `grant all privileges on sfa.* to 'sfa'@'localhost' identified by 'password';`
5. `flush privileges;`

## Todo
- D3 
  - Heatmap
  - Map data
  - Other...?
- HighCharts
  - Bar chart
  - Line chart
  - Bubble chart

## Interesting Branches
We have branched the code to provide usage examples, typically as starting points for other projects.  Here, you can find a list of example branches that you can clone.

To clone a specific branch, you can run the following command: 

`git clone -b [branch name] git@gitli.corp.linkedin.com:ba-hackers/sample_flask_app.git` [name of directory to clone into]

### carabiner-example
The Carabiner example includes an autocomplete data source, a date input, a dropdown select that shows and hides these inputs, bootstrap styling, a table and a line plot. # flask_app_skeleton
