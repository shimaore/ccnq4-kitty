    module.exports = [

`willing-toothbrush` needs to be updated, but basically we allow for the creation of `trace:` documents (as if the willing-toothbrush service was monitoring a DB) and the client that subscribes to the trace gets all updates related to that trace, either from CouchDB (need to write that code probably) or from the servers (i.e. when subscribing to `trace:<id>` you get all the documents related to that trace, not just that document).

      'trace'

`ccnq4-opensips` needs to be updated, these documents are currently called `location` or `locations`, which conflicts with the existing `location` documents used for emergency call routing.

      'register'

Not sure `ccnq4-opensips` actually does anything with those.

      'presentities'

Many ways to create a call:
- call from an endpoint to a number (`huge-play`)
- call from an agent to a number
- (forgot the third one)
Call state data (currently `huge-play`'s `report`) need to be merged here as well, and the fields defined properly.

      'call'

    ]
