App Engine application for the Udacity training course.

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool


## Task 1: Add Sessions to a Conference

The Session class and forms are declared in models.py and the required Endpoints methods are added to conference.py

### Design choices

I tried to keep the design of sessions as simple and neat as possibly - most fields are StringFields except duration and typeOfSession. typeOfSession is an EnumField to provide restriction to formal events. I consider allowing multiple speaker (e.g. set repeated=True) but for simplicity sake, it remains single at the end.

## Task 2: Add Sessions to User Wishlist

Reflected in conference.py

## Task 3: Work on indexes and queries

```python
# sessions that are workshops
sessions = Session.query(Session.typeOfSession == SessionType.WORKSHOP)

# get all sessions holding in a conference
conf = Conference.query().filter(Conference.name=="CONFERENCE NAME")
sessions = Session.query(ancestor=conf.key)
```

## Solve the following query related problem

Let’s say that you don't like workshops and you don't like sessions after 7 pm. How would you handle a query for all non-workshop sessions before 7 pm? What is the problem for implementing this query? What ways to solve it did you think of?

```python
# pseudo code: Earlier than 19:00, not workshop
session.query().filter(Session.startTime<19).filter(~Session.typeOfSession.IN([SessionType.WORKSHOP]))
```

## Task 4:

getFeaturedSpeaker endpoints method is in conference.py