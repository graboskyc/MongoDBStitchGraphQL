# MongoDBStitchGraphQL

# Guide

* Deploy a MongoDB Atlas cluster
* Load the sample dataset (we will be using `sample_mflix` movies database)
* Create a stitch application. This will take up to five minutes to load, then take you to the Stitch application.

![](img/ss01.png)

* Define a rule such that everyone can only read the `sample_mflix.movies` collection

![](img/ss02.png)

* Create a new custom rule by clicking the plus button, choosing the `sample_mflix` database, typing in `opinions` in the collection box, clicking "Create opinions", choose the rule of "Users can only read and write their own data", type `owner` in the field name, then click "Create"

![](img/ss03.png)

* Press the "Review & Deploy Changes" button on the top blue bar, then the green "Deploy" button

* Generate a schema for the `movies` collection by clicking `movies` then "Schema" and we can "Generate Schema" since there is already data in the collection. Then click "Save"

![](img/ss04.png)

* Click on the `opinions` collection and it's schema tab.
* Paste in this new schema:

```
{
  "title": "opinions",
  "properties": {
    "owner": {
      "bsonType": "string"
    },
    "opinion": {
      "bsonType": "string"
    },
    "rated": {
      "bsonType": "double"
    }
  }
}
```

![](img/ss05.png)

* Press the "Review & Deploy Changes" button on the top blue bar, then the green "Deploy" button

* We will now create username/password authentication for users. Click the __Users__ button, then __Providers__, then the __Edit__ button next to __Email/Password__

![](img/ss06.png)

* Enable the provider, choose "automatically confirm users" radio button, choose "Run a password reset function", call the function `reset` and leave everything defaults as this is all outside of scope for today's exercise. Click __Save__

![](img/ss07.png)

* Press the "Review & Deploy Changes" button on the top blue bar, then the green "Deploy" button

* Click the __Add a new user__ button and put in your email address and a password and create the user.