# MongoDBStitchGraphQL

## Initial Setup Guide

* Deploy a MongoDB Atlas cluster
* Load the sample dataset (we will be using `sample_mflix` movies database)
* Create a stitch application. This will take up to five minutes to load, then take you to the Stitch application.

![](img/ss01.png)

* Define a rule such that everyone can only read the `sample_mflix.movies` collection

![](img/ss02.png)

* Create a new custom rule by clicking the plus button, choosing the `sample_mflix` database, typing in `opinions` in the collection box, clicking __Create opinions__, choose the rule of __Users can only read and write their own data__, type `owner` in the field name, then click __Create__

![](img/ss03.png)

* Press the __Review & Deploy Changes__ button on the top blue bar, then the green __Deploy__ button

* Generate a schema for the `movies` collection by clicking `movies` then __Schema__ and we can __Generate Schema__ since there is already data in the collection. Then click __Save__

![](img/ss04.png)

* Click on the `opinions` collection and it's schema tab.
* Paste in this new schema:

```
{
  "title": "opinions",
  "properties": {
    "_id": {
      "bsonType": "objectId"
    },
    "owner": {
      "bsonType": "string"
    },
    "opinion": {
      "bsonType": "string"
    },
    "rated": {
      "bsonType": "double"
    },
    "title": {
      "bsonType": "string"
    }
  }
}
```

![](img/ss05.png)

* Press the __Review & Deploy Changes__ button on the top blue bar, then the green __Deploy__ button

* We will now create username/password authentication for users. Click the __Users__ button, then __Providers__, then the __Edit__ button next to __Email/Password__

![](img/ss06.png)

* Enable the provider, choose "automatically confirm users" radio button, choose __Run a password reset function__, call the function `reset` and leave everything defaults as this is all outside of scope for today's exercise. Click __Save__

![](img/ss07.png)

* Press the __Review & Deploy Changes__ button on the top blue bar, then the green __Deploy__ button

* Click the __Add a new user__ button and put in your email address and a password and create the user.
* Once the user is added, press the copy button next to the user ID. You will need this in future steps.
* Click on the __GraphQL__ button for the next series of steps.

![](img/ss08.png)

## GraphQL Sample Queries
### MOVIE: Random movie
Find a random movie and return just it's ID, title, and release year
```
query {
  movie {
        _id
		title
		year
  }
}
```

### MOVIE: Specific Movie Details
Given a specific title, return just its ID, title, year, rated, and runtime
```
query {
  movie(query:{ title:"Ghostbusters"}) {
    _id
    title
    year
    rated
    runtime
  }
}
```

## GraphQL Sample Mutations
## OPINIONS: Log your opinions
_Replace the GUID with your ID you copied earlier_

```
mutation {
  insertOneOpinions(
    data : { title:"Ghostbusters",
    rated:10,
    opinion:"Greatest movie ever",
    owner:"5e4ea9daa329830aaaee66ef"}
  ) { title, rated }
}
```

```
mutation {
  insertOneOpinions(
    data : { title:"John Wick",
    rated:9.5,
    opinion:"great fight scenes",
    owner:"5e4ea9daa329830aaaee66ef"}
  ) { title, rated, _id, owner }
}
```

## GraphQL Sample Queries
### OPINIONS: Your opinions
_Replace the GUID with your ID you copied earlier_
```
query {
  opinions(query:{owner:"5e4ea9daa329830aaaee66ef"}) {
    _id
		title
		rated
    owner
    opinion
  }
}
```