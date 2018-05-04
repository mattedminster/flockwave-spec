# `SYS` --- System information

## `SYS-PING` --- Check whether a connection is alive

Either party in the connection may send a `SYS-PING` message to the other party to test whether the connection is still alive. Parties receiving a `SYS-PING` message are expected to respond with an [`ACK-ACK`](ack.md#ack-ack-positive-acknowledgment) message as soon as it is practical to do so.

Note that each party may decide whether it wants to send `SYS-PING` messages over the wire periodically. Typically, the message is used to implement "heartbeating" to detect broken connections. If the transport protocol used to convey Flockwave messages implements heartbeating on its own, there is no additional benefit to firing `SYS-PING` messages. However, when Flockwave messages are transmitted over a plain TCP connection, `SYS-PING` messages may be used by either side to detect when the connection was dropped.

**Request fields**

This request has no fields.

**Response fields**
Responses should not be sent with this type; use [`ACK-ACK`](#ack-ack-positive-acknowledgment) instead.

**Example request**
```js
{
    "type": "SYS-PING"
}
```

## `SYS-VER` --- Version number of the server

A `SYS-VER` request retrieves the version number of the server.

**Request fields**

This request has no fields.

**Response fields**

Name | Required? | Type | Description
---- | --------- | ---- | -----------
`name` | no | string | The name of the server. May be used to distinguish between multiple servers running concurrently so the operators know that they are connecting to the right server from the client.
`revision` | no | string | The revision number of the server, if known. This field is optional and can be used to convey more detailed version information than what the `version` field allows; for instance, one could provide the Git hash of the last commit in the server's repository.
`software` | yes | string | The name of the server implementation.
`version` | yes | string | The version number of the server, in major.minor.patch format. The patch level is optional and may be omitted.

**Example request**
```js
{
    "type": "SYS-VER"
}
```

**Example response**
```js
{
    "type": "SYS-VER",
    "name": "CollMot test server",
    "software": "flockwave-server",
    "version": "1.0",
    "revision": "1.0+git:e2a0dc5"
}
```

