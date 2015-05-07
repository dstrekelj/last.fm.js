last.fm JavaScript API
---

### Preface

This project was inspired by [fxb's javascript-last.fm-api](https://github.com/fxb/javascript-last.fm-api). I wholeheartedly recommend using that solution if you require something completely fleshed out.

### About

Currently, this JavaScript 'wrapper' for the last.fm API provides access to only a small portion of available API methods. These are the Album, Artist, and User methods that use unauthenticated calls. It's possible to wrapp all of the other API methods that use unauthenticated calls, so that's going to happen eventually.

API methods that require authentication are not yet supported because the wrapper lacks a way to make 

Keep in mind that all responses are formatted strings and need to be parsed into JSON / XML to be used effectively.

For more information on how to use the last.fm API please read the [official documentation](http://www.last.fm/api/).

At this stage everything is very _bare-bones_ and incomplete, but it does what I need it to do. Pull requests are, of course, welcome.

### Example use

```javascript
/**
 * `apiKey` - Required
 * `apiSecret`- Currently optional as it's not used anywhere
 * `rootUrl` - Optional, defaults to root URL at the time of writing
 * `format` - Optional. Set to `json` for JSON, leave empty for XML
 */
var lfm = new LastFM({
  apiKey    : 'abcdef01234567899876543210fedcba',
  apiSecret : '9876543210fedcbaabcdef0123456789',
  rootUrl   : 'http://ws.audioscrobbler.com/2.0/',
  format    : 'json'
});

/**
 * Grab jimbobby's top 10 artists, print name and playcount to console
 */
lfm.user.getTopArtists({user: 'jimbobby', limit: 10}, function(Response) {
  var artists = JSON.parse(Response).topartists.artist;
  artists.forEach(function(e) { console.log(e.name + '\t' + e.playcount); });
});
```
### TODO

* [User authentication](http://www.last.fm/api/authentication) for services that require authentication
* Add support for all available methods