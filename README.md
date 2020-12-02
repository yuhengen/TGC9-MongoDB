# RESTAURANT
## Find all restaurants that specialize in hamburgers cuisine
```
db.restaurants.find({
    'cuisine': 'Hamburgers'
}, {
    'name':1,
    'borough':1,
    'cuisine':1
}).pretty()
```

## Find all restaurants that specialize in American cuisine and are in the Bronx borough
```
db.restaurants.find({
    'cuisine':'American',
    'borough':'Bronx'
}, {
    'name':1,
    'borough':1,
    'cuisine':1
}).pretty()
```

## Find all restaurants that are located at the street "Stillwell Avenue"
```
db.restaurants.find({
    'address.street':'Stillwell Avenue'
}, {
    'name':1,
    'borough':1,
    'cuisine':1,
    'address.street':1
}).pretty()
```

# MFLIX
## Count how many movies there are
```
db.movies.find().count()
```

## Count how many movies there are released before the year 2000
```
db.movies.find({
    'released': {
        '$lt':ISODate('2000-01-01')
    }
}, {
    'title':1,
    'released':1
}).count()
```
```
db.movies.find({
    'year':{
        '$lt':2000
    }
}).count()
```

## Show the first ten titles of movies produced in the USA
```
db.movies.find({
    'countries':{
        '$in':['USA']
    }
}, {
    'title':1,
    'countries':1
}).pretty().limit(10)
```

## Show the first ten titles of movies not produced in the USA
```
db.movies.find({
    'countries':{
        '$not':{
            '$in':['USA']
        }
    }
}, {
    'title':1,
    'countries':1
}).pretty().limit(10)
```
```
db.movies.find({
    'countries':{
        '$nin':['USA']
    }
}, {
    'title':1,
    'countries':1
}).pretty().limit(10)
```

## Show movies that have at least 3 wins in the awards object
```
db.movies.find({
    'awards.wins':{
        '$gte':3
    }
}, {
    'title':1,
    'awards.wins':1
}).pretty()
```

## Show movies that have at least 3 nominations in the awards object
```
db.movies.find({
    'awards.nominations':{
        '$gte':3
    }
}, {
    'title':1,
    'awards.nominations':1
}).pretty()
```

## Show movies that cast Tom Cruise
```
db.movies.find({
    'cast':{
        '$in':['Tom Cruise']
    }
}, {
    'title':1,
    'cast':1
}).pretty()
```

## Show movies that are directed by Charles Chaplin
```
db.movies.find({
    'directors':{
        '$in':['Charles Chaplin']
    }
}, {
    'title':1,
    'directors':1
}).pretty()
```

## Pattern matching (Same as LIKE in SQL)
Find all movies that have `Star Wars` (regardless of casing) in it

```
db.movies.find({
    'title':{
        '$regex':"Star Wars",
        '$options':'i'
    }
}, {
    'title':1
}).pretty()
```

## Doing Logical OR
Find movies directed by Steven Spielburg and before year 1999 or directed by Charles Chaplin

```
db.movies.find({
    '$or':[
        {
            'directors':'Steven Spielberg',
            'year': {
                '$lt':1999
            }
        },
        {
            'directors':'Charles Chaplin'
        }
    ]
},{
    'title':1,
    'directors':1,
    'year':1
}).pretty()
```

# WEATHER
## Count how many records there are of wind speed with rate higher than 5
```
db.data.find({
    'wind.speed.rate':{
        '$gt':5
    }
}).count()
```

## Count how many records there are of wind speed with rate higher than 5 but is not 999.9
```
db.data.find({
    'wind.speed.rate':{
        '$gt':5,
        '$ne':999.9
    }
}).count()
```
# Design Swimming coach App
## Allows parent to book a slot for a coach

**Sessions**
* available slots
    * venue
        * address
            * street
            * building name
            * postal code
    * coach
        * first name
        * last name
        * gender
        * awards
    * date and time

**Bookings**
* each bookings

db.students.insertMany([
    {
    'name':'Jane Doe',
    'age':13,
    'subjects':'Defense Against the Dark Arts','Charms','History of Magic',
    'date_enrolled': ISODate('2016-05-13')
    },{
    'name':'James Verses',
    'age':14,
    'subjects':'Transfiguration','Alchemy',
    'date_enrolled': ISODate('2015-06-15')
    },{
    'name':'Jonathan Goh',
    'age':12,
    'subjects':'Divination','Study of Ancient Runes',
    'date_enrolled': ISODate('2017-04-16')
    }

])