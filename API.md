# API

## rails service (default port 3000)

### `POST api/v1/applications`

Creates new application.

Request:

```js
{
    name:   String
}
```

Response:

```js
{
    name:   String,
    token:  String
}
```

Status codes:

```yaml
201:
  Application created.
400:
  Can't proccess parameters
```

### `GET api/v1/applications/:token`

Get application by token.

Response:

```js
{
  name: String,
  token: String
}
```

Status codes:

```yaml
200:
  Application found and returned.
404:
  Application with this token not found.
```

### `PATCH api/v1/applications/:token`

Edit application's name.

Response:

```js
{
  name: String
}
```

Status codes:

```yaml
200:
  Application Edited.
404:
  Application with this token not found.
400:
  there's something wrong in the request body.
```

### `DELETE api/v1/applications/:token`

Delete an application.

Status codes:

```yaml
204:
  Application deleted successfully.
404:
  Application with this token not found.
```

### `GET api/v1/applications/:token/chats`

Get all chats for specific application.

Response:

```js
{
  [
    per_app_id: Number,
    message_count: Number
  ]
}
```

Status codes:

```yaml
200:
  Found chats for application successfully.
404:
  Application with this token not found.
```

### `GET api/v1/applications/:token/chats/:chat_num`

Get a specific chat.

Response:

```js
{
  per_app_id: Number,
   message_count: Number
}
```

Status codes:

```yaml
200:
  Found chat.
404:
  Chat not found.
```

### `DELETE api/v1/applications/:token/chats/:chat_num`

Delete a specific chat.

Status codes:

```yaml
204:
  Chat deleted successfully.
404:
  Chat found.
```

### `GET api/v1/applications/:token/chats/:chat_num/messages`

Get all message for specific chat.

Response:

```js
{
  [
    per_chat_id: Number,
    body: String
  ]
}
```

Status codes:

```yaml
200:
  Found messages for chat successfully.
404:
  Chat with this token not found.
```

### `GET api/v1/applications/:token/chats/:chat_num/messages/:message_num`

Get a specific message.

Response:

```js
{
  per_chat_id: Number,
   body: String
}
```

Status codes:

```yaml
200:
  Found message.
404:
  Message not found.
```

### `DELETE api/v1/applications/:token/chats/:chat_num/messages/:message_num`

Delete a specific message.

Status codes:

```yaml
204:
  Message deleted successfully.
404:
  Message found.
```

## go service (default port 8000)

### `POST api/v1/applications/:application_token/chats`

Create new chats.

Response:

```js
{
  number_of_chats: Number,

}
```

Status codes:

```yaml
201:
  Chat created.
400:
  Can't proccess parameters.
404:
  Can't find application with given token.

```

### `Post api/v1/applications/:application_token/chats/:chat_num/messages`

Create new message.

Response:

```js
{
  number_of_messages: Number,

}
```

Status codes:

```yaml
201:
  Message created.
400:
  Can't proccess parameters.
404:
  Can't find application or chat with specified token and chat_num.

```