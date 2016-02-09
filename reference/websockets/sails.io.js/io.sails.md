# The `io.sails` object

### Overview

The `io.sails` object exposes global configuration options for the `sails.io.js` library.  Most of the options are used as settings when connecting a client socket to the server.  `io.sails` also provides a `.connect()` method used for creating new socket connections.

> The `sails.io.js` library waits for one cycle of the event loop before automatically connecting a socket (if `autoConnect` is enabled; [see below](http://sailsjs.org/documentation/reference/web-sockets/socket-client/io-sails#?autoconnect)).  This is to allow any `io.sails` global properties that you specify to be set before the socket connects.  However, in order to ensure that the `io.sails` properties are read before connection, you should put the code setting those properties immediately after the `sails.io.js` script include:
```
<script src="/js/dependencies/sails.io.js"></script>
<script type="text/javascript">io.sails.url="http://myapp.com"</script>
...other scripts...
```

### The `.connect()` method

If [`io.sails.autoconnect`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/io-sails#?autoconnect) is `false`, or if you need to create more than one socket connection with the `sails.io.js` library, you do so via `io.sails.connect([url], [options])`.  Both arguments are optional, and the value of the `io.sails` properties (like `url`, `transports`, etc.) are used as defaults.  See the [SailsSocket properties reference](http://sailsjs.org/documentation/reference/web-sockets/socket-client/sails-socket/properties) for options.

### `autoConnect`

When the `io.sails.autoConnect` is set to `true` (the default), the library will wait one cycle of the event loop after loading and then attempt to create a new [`SailsSocket`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/sails-socket) and connect it to the URL specified by `io.sails.url`.  When used in the browser, the new socket will be exposed as `io.socket`.  When used in a Node.js script, the new socket will be attached as the `socket` property of the variable used to initialize the `sails.io.js` library.

### `environment`

Use `io.sails.environment` to set an environment for `sails.io.js`, which affects how much information is logged to the console.  Valid values are `development` (full logs) and `production` (minimal logs).

### Other properties and defaults

The other properties of `io.sails` are used as defaults when creating new sockets (either via autoconnect or [`io.sails.connect()`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/io-sails#?the-connect-method)).  See the [SailsSocket properties reference](http://sailsjs.org/documentation/reference/web-sockets/socket-client/sails-socket/properties) for a full list, as well as a table of the default `io.sails` values.  Here are the most commonly used properties:

  Property          | Type       | Default   | Details
 ------------------ |----------| --------- | :-------:
 `url`              | ((string)) | Value of [`io.sails.url`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/sails-socket/properties#?iosails-defaults) | The URL that the socket is connected to, or will attempt to connect to.
 `transports`       | ((array))  | Value of [`io.sails.transports`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/sails-socket/properties#?iosails-defaults) | The transports that the socket will attempt to connect using.  Transports will be tried in order, with upgrades allowed: that is, if you list both "polling" and "websocket", then after establishing a long-polling connection the server will attempt to upgrade it to a websocket connection.  This setting should match the value of `sails.config.sockets.transports` in your Sails app.
`headers` | ((dictionary)) | Value of [`io.sails.headers`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/sails-socket/properties#?iosails-defaults) | Dictionary of headers to be sent by default with every request from this socket.  Can be overridden via the `headers` option in [`.request()`](http://sailsjs.org/documentation/reference/web-sockets/socket-client/io-socket-request).




<docmeta name="displayName" value="io.sails">
<docmeta name="pageType" value="property">