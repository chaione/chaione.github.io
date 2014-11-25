---
title: Feeds
layout: default
---
#Contextual Engine

##FEEDS

Feeds are specially crafted, application-specific URLs generated by ContextHub that let you trigger your own custom events from any web browser, JavaScript script, Arduino, Raspberry Pi, or other IoT device. Feeds are perfect for integrating new platforms not yet directly supported by our SDKs into your own applications.

###Creating

Creating a feed is simple. In the developer portal, select an app, then click on *Settings*, then the *Feeds* tab to see all the feeds for you app. To create a new feed, click the *New Feed* button and type in a name of the feed. A generated feed looks like this:

`https://app.contexthub.com/api/feeds/:token/:event_name`

- `:token` - random alphanumeric string generated by ContextHub tying the events for the feed directly to your app
	- Example: `1782914xneuuoy26b6g45swco`
- `:event_name` - name of the event which will match the context rule during rule processing
	- Example: `arduino_event`

So the full URL for a feed linked to your app that would post the `arduino_event` would be:

`https://app.contexthub.com/api/feeds/1782914xneuuoy26b6g45swco/arduino_event`

###Posting

To use a feed, you need to generate an HTTP POST request with the appropriate token and event name, along with posting the JSON body that represents the data for your event. The web request should have the `Content-Type` header set to `application/json` so the body is parsed correctly. A web tool like [Hurl.it](http://www.hurl.it) is a great way to test that your feeds are working correctly and you are passing the correct data to a context rule.