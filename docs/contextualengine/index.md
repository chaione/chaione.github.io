---
title: Contextual Engine
layout: default
---

# Contextual Engine
{: #contextual-engine}

The contextual engine is the center of ContextHub, adding dynamic capabilities to events generated by your apps through context rules. Context rules are written in JavaScript, and are triggered by events. When you create a rule (also called 'Context'), you specify an event type. As events are coming in, if their event type matches a rule, it will be executed. Note that it is entirely possible to have more than one rule associated with a certain event type. In this case, multiple rules will execute in parallel.

To make Context Rules more useful, ContextHub provides a number of pre-existing objects that you can interact with when one of your context rules executes:

- [console](#console): Logs activity
- [event](#event): Contains the data from the event that triggered the rule
- [http](#http): Allows you to send http get/post requests
- [vault](#vault): Lets you persist data in ContextHub

Details about each object are presented below:

<a name="console" data-magellan-destination="console-log"></a>

## Console
The *console* object allows you to log activity inside your context rule.

### Console Methods

| Method    | Description |
|-----------|-------------|
| [log](#console-log)   | Logs a message to the 'logs' area in the Developer Portal. |

<a name="console-log" data-magellan-destination="console-log"></a>

---

#### Log

Logs the message to the console. You can see the logs from the *Logs* screen in the [developer portal](https://app.contexthub.com).

##### Syntax
`console.log(message)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| message   | Required. Message to log to the console. |

##### Return Value
Nothing.

##### Example
{% gist CHLibrarian/25f12ebc450a8dba7027 %}

<a name="event" data-magellan-destination="event"></a>

---

## EVENT
The `event` object contains the data from the event that triggered the execution of the context rule. The `event` object is read-only and contains the following properties:

| Property   | Description |
|------------|-------------|
| name       | The name of the event. This matches the event type of the context rule. |
| data       | The data object contains all the properties relevant to this event type. See below for specific structures. |
| id         | A unique identifier for this event. |
| created_at | An ISO8601 timestamp of when the event was received by the server. |


<a name="event-sampleevent" data-magellan-destination="event-sampleevent"></a>

### Trigger Events

Trigger events are events generated by posting an event through a trigger endpoint for web browsers, servers, JavaScript scripts, and IoT-like devices like the Raspberry Pi or Arduino. All events have a `name` key, which is the 'event type' portion of the trigger URL endpoint that matches the rule and allows it to execute, and a `data` key that contains the custom data structure passed in the body of the POST request. 

<p class="p-indent-30">Below is a sample of a data structure of a custom event, taken from the [Awareness](/samples/ios/awareness) context rule sample app.</p>

{% gist CHLibrarian/57a43d174de887c0b778 %}

<a name="event-tick" data-magellan-destination="event-tick"></a>

### Tick

The `tick` event is a special event that is automatically executed once every minute in the ContextHub server. Using the JavaScript `Date()` object and checking the time, this allows you the ability to execute commands in ContextHub even with the *absence* of any events on the server. So instead of your server code simply being reactive to devices, it can be a proactive part of your applications.

{% gist CHLibrarian/109cad3805c2650fe9f0 %}

<a name="event-customevents" data-magellan-destination="event-customevents"></a>

### Sample Event

Here is the structure of a sample event:
{% gist r-moctezuma/ae7a6843fe9e02316d0d9401a8c3f6be %}


<a name="http" data-magellan-destination="http"></a>

---

## HTTP
The *http* object allows you to send http requests to external services in a context rule. This allows you
to send data to external servers when interesting events occur inside ContextHub. You will see the status
of your request in your logs, but you will not be able to do anything with the response.

### http methods

| Method    | Description |
|-----------|-------------|
| [get](#http-get)   | Makes a http GET request to the specified url. |
| [post](#http-post)   | Makes a http POST request to the specified url. |

<a name="http-get" data-magellan-destination="http-get"></a>

---

#### Get

Allows you to perform an http GET request to a specific URL. You can specify optional query parameters and headers with the *params*, and *headers* parameters. These need to be in the form of JSON strings.

##### Syntax
`http.get(url, params, headers)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| url       | Required. The url you are making the request to. |
| params    | Optional. Stringified JSON of any query parameters that you want to include. |
| headers   | Optional. Stringified JSON of any request headers that you want to include. |

##### Return Value
Nothing.

##### Example
{% gist CHLibrarian/9a5e0f673a526ee790a2 %}

<a name="http-post" data-magellan-destination="http-post"></a>

---

#### Post

Allows you to perform an http POST request to a specific URL. You can specify optional headers with the  *headers* parameter. This needs to be in the form of a JSON string.

##### Syntax
`http.post(url, body, headers)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| url       | Required. The url you are making the request to. |
| body      | Optional. The body of the post request. |
| headers   | Optional. Stringified JSON of any request headers that you want to include. |

##### Return Value
Nothing.

##### Example
{% gist CHLibrarian/ae16587c627cf3e8d520 %}


<a name="vault" data-magellan-destination="vault"></a>

---

## Vault
The *vault* object provides access to the vault document store.

### vault methods

| Method    | Description |
|-----------|-------------|
| [create](#vault-create)   | Adds a new document to the vault. |
| [find](#vault-find)       | Retreives a document from the vault via id. |
| [allTagged](#vault-alltagged) | Finds vault objects matching **all** of the given tags |
| [anyTagged](#vault-anytagged) | Finds vault objects matching **any** of the given tags |
| [search](#vault-search) | Finds vault objects containing the given term.
| [keyPath](#vault-keypath) | Finds vault objects with the given key path. |
| [update](#vault-update)    | Updates an existing vault object with new information  |
| [destroy](#vault-destroy)   | Deletes a vault object from the system |

<a name="vault-create" data-magellan-destination="vault-create"></a>

---

#### Create
Stores the given json data in the vault with the given tags.

##### Syntax
`vault.create(data, tags)`

##### Parameter Values

| Parameter    | Description |
|--------------|-------------|
| data         | Required. Stringified JSON of the data you want to store in the vault. |
| tags         | Required. A comma separated string of tags to associate with the vault object. If you don't want to tag the vault object, you can pass in null or "".|

##### Return Value
The id of the newly created vault object.

##### Example
{% gist CHLibrarian/a098fd2a92e835982b20 %}

<a name="vault-find" data-magellan-destination="vault-find"></a>

---

#### Find
Retreives a document from the vault via id.

##### Syntax
`vault.find(id)`

##### Parameter Values

| Parameter  | Description |
|------------|-------------|
| id         | Required. The id of the vault object to find. |

##### Return Value
A vault object.
{% gist CHLibrarian/f03d82ad1e2e1c4b5d0c %}

| Property   | Description |
|------------|-------------|
| data       | Your data is stored under the data propery. |
| vault_info | Object containing metadata about the vault object.|

| vault_info Properties | Description |
|-----------------------|-------------|
| **id** | The vault object id. |
| **tags** | Array of tags assigned to the vault object. |
| **created_at** | Timestamp of when the object was created. |
| **updated_at** | Timestamp of when the object was last updated. |
| **tag_string** | Tags as a comma separated string |

##### Example
{% gist CHLibrarian/08e7a097a018ae13b8b2 %}

<a name="vault-alltagged" data-magellan-destination="vault-alltagged"></a>

---

#### All Tagged
Finds vault objects that contain *all* the specified tags.

##### Syntax
`vault.allTagged(tags)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| tags      | Required. A string containing the tag(s) to search for. Multiple tags can be searched for by separating them with commas. Results will contain vault objects that match **all** the specified tags. |

##### Return Value
An array of vault objects.
{% gist CHLibrarian/a9409c08102b01815250 %}

##### Example
{% gist CHLibrarian/f95de5fabe8af80431ce %}

<a name="vault-anytagged" data-magellan-destination="vault-anytagged"></a>

---

#### Any Tagged
Finds vault objects that contain *any* of the specified tags.

##### Syntax
`vault.anyTagged(tags)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| tags      | Required. A string containing the tag(s) to search for. Multiple tags can be searched for by separating them with commas. Results will contain vault objects that match **any** the specified tags. |

##### Return Value
An array of vault objects.
{% gist CHLibrarian/a9409c08102b01815250 %}

##### Example
{% gist CHLibrarian/f95de5fabe8af80431ce %}

---

<a name="vault-search" data-magellan-destination="vault-search"></a>

#### Search
Finds all vault objects that contain the given term. You can use the following search operators in your queries to fine tune your results. You can use parentheses to set operator precedence.

| Operator | Example |
|----------|---------|
| **Not**  | !term   |
| **And**  | term1 & term2 |
| **Or**   | term1 \| term2 |

##### Syntax
`vault.search(term)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| term      | Required. A string containing the term to search for. Any documents containing the term will be returned. |

##### Return Value
An array of vault objects.
{% gist CHLibrarian/a9409c08102b01815250 %}

##### Example
{% gist CHLibrarian/ccd10b6bf887a37037fc %}

<a name="vault-keypath" data-magellan-destination="vault-keypath"></a>

---

#### KeyPath
Finds all vault objects that have the specified key path. If a value is provided, then documents that have the value
at the key path will be returned.

##### Syntax
`vault.keyPath(key, value)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| key       | Required. A string containing the key to search for. Use dot notation *'address.city'* for specifying a nested key. |
| value     | Optional. If provided documents that match the value at the key will be returned. Otherwise, all documents that contain the key will be returned. |

##### Return Value
An array of vault objects.
{% gist CHLibrarian/a9409c08102b01815250 %}

##### Example
{% gist CHLibrarian/833335fce9bb9e522407 %}

<a name="vault-update" data-magellan-destination="vault-update"></a>

---

#### Update
Replaces the vault object at the given id with the given data.

##### Syntax
`vault.update(id, data, tags = nil)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| id        | Required. The id of the vault object to update. |
| data      | Required. Stringified JSON of the data you want to store in the vault. |
| tags      | Optional. A comma separated string of tags to associate with the vault object. If you don't want to update the tags, you can omit this parameter. |

##### Return Value
Nothing.

##### Example
{% gist CHLibrarian/cd7dc04e6624ebbc35e2 %}

<a name="vault-destroy" data-magellan-destination="vault-destroy"></a>

#### Destroy
Deleting a vault items only requires passing the id to the *vault* object. The vault item is deleted from ContextHub.

##### Syntax
`vault.destroy(id)`

##### Parameter Values

| Parameter | Description |
|-----------|-------------|
| id        | Required. The id of the vault object to delete. |

##### Return Value
Nothing.

##### Example
{% gist CHLibrarian/a55f094872efed65ad3b %}


