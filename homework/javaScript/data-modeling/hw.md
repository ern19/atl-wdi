[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Data Modeling with JavaScript

Every computer program deals with managing data. How you choose to represent
these data within your program can have far-reaching implications on every other
part of your application; consequently, reversing those decision becomes more
and more costly over time, as the program becomes more complex. For this reason,
thinking carefully in advance about how you want to model your data within your
application can pay very big dividends.

## Choosing Entities/Abstractions

One of the first challenges in modeling data is deciding what data to model.
Let's consider a specific example: a laptop. Suppose that you need to represent
a laptop in an application. What attributes are most important to include in our
data model?

As it turns out, the answer to that question depends heavily on what the
application will do and how it will be used. If the application is for selling
laptops, we might be pick the following attributes.

  > A Laptop has...
  > - a sale price
  > - a brand name
  > - an amount of RAM, in GB
  > - a disc size, in GB
  > - a processor speed, in GHz
  > - a monitor size, in inches
  >
  > e.g.

  ```js
  var laptop = {
    salePrice: 1000,
    brand: 'Lenovo',
    RAM: 8,
    disc: 60,
    processor: 2.5,
    monitorSize: 12
  }
  ```

However, if the application will be used for _manufacturing laptops_,
things like sale price suddenly become much less relevant; instead, a laptop in
that kind of app might have information about materials costs, % completion,
or the factory and assembly line on which the laptop was built.

Take a look at each of the app descriptions below. For each description,
create a rough data model for the app by listing at least two relevant
entities/abstractions (e.g. Laptop, above) that the app might use, and giving
them each several properties that make sense for that use case.
Please also give a short explanation (1 - 2 sentences) of why these choices make
sense for the use case of the app.

### 1. To-Do List

This app will be an app for tracking and managing tasks. Not only will it keep
track of whether tasks have been completed, it will also keep track of
how long each task took to complete. Tasks can be grouped into 'projects' to
keep them organized.

var tasks = {
  title: 
  description:
  dateStart
  dateDue:
  projectType:
  duration:
  completionStatus:
}
var projects = {
  projectName:
  tasksForProject:
  projectStart
  projectEnd:
}
This would allow you to create detailed tasks with start/end dates as well as time to complete them. They can be grouped into projects that can have their own start and end dates.

### 2. Photo Sharing App

In this app, users can upload photos to their accounts and share them with others. These photos can be grouped into albums.

var users = {
  username:
  aboutMe:
  pics: 
  albums:
}

var photos = {
  title: 
  datePosted:
  hostURL:
}

var albums = {
  title:
  photoSet:
}
Each user would have a profile page with all of their albums and photos. The albums can be customized to have particular photos grouped together. 
### 3. Home Automation Manager

This app will be a tool for managing a home automation system; it will keep
track of the time and temperature of the house that it monitors, and use that
information to turn on and off different lights and adjust the thermostat up
and down.

const lights = {
  timesToActivate:
  timesToDeactivate:
  lightLocations:
  brightness:
}

const temp = {
  defaultTemp:
  tempAtCertainTimes: 
  
}
Users can set a default temp, and set it to a different one at different parts of the day. Users can adjust the lights to turn on or dim at certain parts of the day as well.
### 4. Sneaker Store

This app will allow customers to browse a list of products (sneakers, in this
case), add those products to a cart, and save that cart as a past order once the
purchase is complete.

var products = {
  description:
  price:
  colors: 
  brand:
  search:
}
var users = {
  email:
  billingInfo:
  mailingInfo:
  cartsSaved:
}
var checkout = {
  name: 
  mailingAdd:
  billingInfo:
  orderDetails:
}
Users can search through all the products by a particular brand or color. Users can save their info for repeat orders
## Representing Abstractions in Code

Once you've chosen the abstractions that your app will use, the next step is to
figure out how to actually represent those abstractions in code. The same
abstraction can often be represented in multiple different ways, and there may
be trade-offs in speed and simplicity that come from using one representation
vs another.

### 5. Subway System

Suppose that you're building an app that tells travelers how many stops they
need to travel to get from one station to another. Two abstractions that you
decide to use to model your application's data are Stations and Rail Lines, with
the following properties:

A Station has:
-   a name
-   a description

A Rail Line has:
-   a name
-   a set of stations that it hits

The team has decided to represent these abstractions in the following way.

```js
// Station
var exampleStation = {
  name: 'Downtown Crossing',
  description: "Downtown Crossing is a shopping district that is a small part of downtown Boston, Massachusetts, located due east of Boston Common and west of the Financial District..."
};

// Rail Line
var exampleLine = {
  name: 'Green Line',
  northStation: {
    name: 'North Station',
    description: "North Station is a major transportation hub located at Causeway and Nashua Streets in Boston, Massachusetts, United States...."
  },
  haymarket: {
    name: 'Haymarket',
    description: "Haymarket is an MBTA subway station serving the Green and Orange lines, located at the corner of Congress and New Sudbury streets in downtown Boston, Massachusetts...."
  },
  governmentCenter: {
    name: 'Government Center',
    description: "Government Center is an area in downtown Boston, centered on City Hall Plaza. Formerly the site of Scollay Square, it is now the location of Boston City Hall..."
  }
};

// Stop and line descriptions from Wikipedia (https://en.wikipedia.org)
```

What are some advantages and disadvantages of choosing these representations? Please give at least one example of each.

It has descriptions of each station and where they're located, which is good. However, if the app is supposed to tell you where to get off, or how many stops are left to your destination, it doesn't appear to have a way to tell you that as currently written.

### 6. Doctor Appointment App

Consider an app for helping patients and doctors schedule appointments.

A Patient has:
-   a given name
-   a surname
-   a date of birth

A Doctor has:
-   a given name
-   a surname
-   a specialty
-   an address

An Appointment has:
-   a date
-   a time

The team has not yet decided how to represent the relationship between doctors,
patients, and appointments, so they've put together two different
alternatives.

#### Option 1

```js
var examplePatient = {
  givenName: 'John',
  surname: 'Doe',
  dateOfBirth: '1992-11-03'
};
var exampleAppointment = {
  date: '2016-12-15',
  time: '13:00',
  patient: {
    givenName: 'Jane',
    surname: 'Doe',
    dateOfBirth: '1980-06-13'
  }
};
var exampleDoctor = {
  givenName: 'Alphonse',
  surname: 'Cula',
  specialty: 'phlebotomy',
  appointments: [
    {
      date: '2015-10-31',
      time: '00:00',
      patient: {
        givenName: 'Lucy',
        surname: 'Westenra',
        dateOfBirth: '1976-06-06'
      }
    },
    {
      date: '2016-10-31',
      time: '00:00',
      patient: {
        givenName: 'Mina',
        surname: 'Murray',
        dateOfBirth: '1989-09-09'
      }
    }
  ]
};
```

#### Option 2

```js
var exampleDoctor = {
  givenName: 'John',
  surname: 'Dorian',
  specialty: 'internal medicine'
};
var examplePatient = {
  givenName: 'Jordan',
  surname: 'Sullivan',
  dateOfBirth: '1978-12-01'
};
var exampleAppointment = {
  date: '2009-04-15',
  time: '19:00',
  doctor: {
    givenName: 'Jan',
    surname: 'Itor',
    specialty: 'psychology'
  },
  patient: {
    givenName: 'Ladinia',
    surname: 'Williams',
    dateOfBirth: '1980-01-01',
  }
}
```

What are some relative advantages and disadvantages of each representation?
Under what circumstances might one representation be a better choice than the
other? Are there any circumstances in which the other representation might be
the better choice?

In the first approach, it seems like it would be difficult to track the appointments of individual patients since they all branch off the individual doctors. If the app was solely for doctors tracking their own individual appts it might be a good choice.

In the second approach, the patients and doctors are separate objects, so I would think that would be easier to keep track of both doctors and patients.

## Tying It Together

### 7. Tic-Tac-Toe

You've been tasked with building an in-browser tic-tac-toe game.

a.  What are some possible entities that your application might use to model its
    data? Please pick at least two, with at least two properties apiece.

GameBoard 
  Declare a size
  Make clickable squares
  Define moves

Players 
  Define players 1 & 2
  Player 1 = X, player 2 = O

ScoreBoard //To keep track of games won and lost
  wins:
  losses:

Moves 
  //18 possible moves, x or o in each of the 9 squares
}

b.  How might those entities be represented in JavaScript code?

 var gameBoard = { 
  size:
  //9 individual squares
  clickableSquares: {
    blank:
    x:
    o:
  }
  xsAndOs:
}
var players = {
  playerOne: "X"
  playerTwo: "O"
}
var scoreBoard { //To keep track of games won and lost
  wins:
  losses:
}
var moves = {
  //18 possible moves, x or o in each of the 9 squares
}

c.  Justify your choices in a) and b). Why these entities? Why these
    representations?

You obviously have to have 2 players for tic-tac-toe and you have to make it so players can effectively take turns. The app has to generate the board to start play, and there are 18 possible moves for the players to make: each square can be either an x or an O. It would make sense for each square to have a blank state, an x state, and an o state. I would then write some sort of conditional to execute when there are 3 x's or o's in a row.
