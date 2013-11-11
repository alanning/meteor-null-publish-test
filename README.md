meteor-null-publish-test
========================

A test to illustrate whether collections null-published to all clients are available at client load.

## Test

```bash
git clone https://github.com/alanning/meteor-null-publish-test
cd meteor-null-publish-test
meteor
```
Open browser to http://localhost:3000/
Check console for output.

```
Player count = 0
Player count = 6
```

## Result

This shows that data that is null-published is not automatically available at client Meteor.startup.  

The could present a problem in certain circumstances since there is no 'ready' callback for null-publish cases, the client has no way to reliably tell when the data has been loaded.

## Workarounds

Use a session variable to emulate the 'ready' state.  Set it to true either in a Deps.autorun which continually checks the collection for a value or record count, or after a set period of time has expired.

null-publish means:

```js
Meteor.publish(null, function () {
  // this data will be sent to every client automatically
})
```
