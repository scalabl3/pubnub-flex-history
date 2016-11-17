# pubnub-flex-history
A Javascript History wrapper for flexible history calls, automatically handling any paging.

*In all the methods, an unix epoch timestamp or a PubNub 17 digit timetoken can be provided where timetokens are expected.*

## Include

Uncompressed

```javascript
<script src="//cdn.rawgit.com/scalabl3/pubnub-flex-history/v1.05/pubnub-flex-history.js"></script>
```

Compressed
```javascript
<script src="//cdn.rawgit.com/scalabl3/pubnub-flex-history/v1.05/pubnub-flex-history-min.js"></script>
```

## test.html ##

To view the results, open the page and the debug console in your browser.

[Test Page](http://scalabl3.github.io/pubnub-flex-history/test.html)

(getall operation is disabled in the test, because it retrieves about 85,000+ messages,
about 10MB worth)

## Setup Example

Pretty straightforward here:

* Get the PubNub Javascript SDK
* Get the pubnub_flex_history from this repo (CDN url provided via rawgit)
* Add the method to your instantiated pubnub object


```javascript
<script src="//cdn.pubnub.com/pubnub-3.7.14.js"></script>
<script src="//cdn.rawgit.com/scalabl3/pubnub-flex-history/v1.05/pubnub-flex-history-min.js"></script>

<script>
  // Call Init first to create a PubNub instance, then add the wrapper method to that object
  var p = PUBNUB.init({
    publish_key: 'demo',
    subscribe_key: 'demo'
  });

  // ** REQUIRED ** Add flex_history method to your PubNub object
  p.flex_history = pubnub_flex_history;

  // Example of a generic callback, but of course you can use your own
  var flex_history_callback = function(result) {
    if (!result.error) {
      console.log(result.operation + " completed", result);
    }
    else {
      console.warn(result.operation + " failed", result);
    }
  }
</script>
```

## Usage Options ##

### general ###

The general usage follows as:

    p.flex_history(options_object, completed_callback)

options_object requires a channel name, and a command which is one of [last, since, between, at, getrange]

```javascript
{
  channel: [channelname]
}
```

### last ###

Gets the last n messages from the channel.

```javascript

// get last 30 messages
var options = {
  channel: 'AAPL',
  last: 30
}

p.flex_history(options, flex_history_callback);

```

### before ###

Gets the last n messages from the channel.

```javascript

var before = 1426010693;

// get last 30 messages
var options = {
  channel: 'AAPL',
  before: before
  msgcount: 30
}

p.flex_history(options, flex_history_callback);

```

### since ###

Get all messages since epoch timestamps or PubNub timetoken.

```javascript

var since = 1426010693;

var options = {
  channel: 'AAPL',
  since: since
}

p.flex_history(options, flex_history_callback);

```

### upto ###

Get all messages from first message in channel "up to" epoch timestamps or PubNub timetoken.

```javascript

var upto = 1426010693;

var options = {
  channel: 'AAPL',
  upto: upto
}

p.flex_history(options, flex_history_callback);

```

### between ###

Get all messages between epoch timestamps or PubNub timetokens.

```javascript

var options = {
  channel: 'AAPL',
  between: [1426010693, 1426021664]
}

p.flex_history(options, flex_history_callback);

```

### at ###

Get single nearest or exact message at epoch timestamp or PubNub timetoken.

```javascript

var options = {
  channel: 'AAPL',
  at: 14259785889989920
}

p.flex_history(options, flex_history_callback);

```

### getrange ###

Get the start and end DateTime range of the channel, timetoken of first message and timetoken of most recent message.

```javascript

var options = {
  channel: 'AAPL',
  getrange: true
}

p.flex_history(options, flex_history_callback);

```

### getall ###

Get all the history available on the channel.

```javascript

var options = {
  channel: 'AAPL',
  getall: true
}

p.flex_history(options, flex_history_callback);

```



