# OpenBUMP

[![Build Status](https://travis-ci.org/BumpConductor/OpenBUMPS.svg?branch=master)](https://travis-ci.org/BumpConductor/OpenBUMPS)

---

## Table of Contents
  * [Overview](#overview)
  * [Data Model](#data-model)
  * [Installation](#installation)

---

## Overview <a id="overview"></a>

Web App consisting of:

- MongoDB databse at (mongodb://<dbuser>:<dbpassword>@ds061246.mlab.com:61246/open_bump)
- Python backend using Flask micro framework
- Nginx proxy servering static resources and routing REST requests to Flask
- Google Polymer Front-end

Currently the polymer frontend is started. Temporarily it can be server with built in polymer serve command.

I have set up a free mongoDB database online. There is no data in it yet. The first create command with create the database, collection and document in one go.

Nginx - to do

Flask REST server - to do

MongoDB - server set-up

---

## Data Model <a id="data-model"></a>

Data to be stored in a Document Store - MongoDB.

The database will contain 3 collections:
- Bumps
- Users
- Solvers

### Bumps Documents Structure

- id	
- Title
- Description
- Submitter -> user id in users
- Date created
- Date last updated
- Solver -> solver id in Solvers
- votes -> user ids in users

JSON:

``` json
    {
	    _id: 1223456548,
	    title: "Kitten Damage to furniture",
	    description: "Kittens can ruin stuff",
	    submitter: 46464784993,
	    created_date: "2016-10-19T23-45-00",
	    last_updated: "2016-11-19T10-45-00",
		solver: 36637300,
		votes: [373878703,
				478940404,
				575003627,
				500037373]

    }
```


### Users Document Structure

- id
- username
- First Name
- Last Name
- Email
- Avatar
- Bumps -> Bump ids in Bumps

JSON:

``` json
    {
	    _id: 1223456548,
	    username: "kcarroll",
	    first_name: "Ken",
	    last_name: "Carroll",
	    email: "kcarroll@hotmail.com",
	    avatar: "/avatars/smiley.jpg",
		bumps: [373878703,
				478940404,
				575003627,
				500037373]

    }
```


### Solvers Document Structure

- id
- Name
- Address
- url
- Info Email
- admins -> user ids in users
- Bumps -> Bump ids in Bumps

JSON:

``` json
    {
	    _id: 1223456548,
	    Name: "Ken Corp",
	    Address: {
					street1: "Central Street",
					street2: "",
					town: "Haarlem",
					post_code: "1987XT"
				},
	    url: "kencorp.com",
	    info_email: "info@kencorp.com",
		admins: [373878703,
				478940404,
				575003627,
				500037373],
		bumps: [373878703,
				478940404,
				575003627,
				500037373]

    }
```

---

## Installation <a id="installation"></a>

### Pre-requisites

- Install latest NodeJS LTS version
- Create a personal development project on firebase and enable google authentication on it

### Install and run

- Clone from github: https://github.com/BumpConductor/OpenBUMPS.git
- cd into the repo folder
- set up a local configuration to point to your personal development project
    - `cp /config/production.json /config/local.json`
    - Then update the settings in `/config/local.json` to match your personal firebase project
- On the command line
    - `npm install`
    - `npm run bower -- install`
    - `npm deploy`
        - this will deploy the rules as well as the website to your personal firebase project
    - `npm start`
        - this will start a local webserver but it will still point to the firebase database (which is why the rules should be deployed first)
- Open a browser and navigate to `http://localhost:8080`

