---
layout: page
title:  "Integrating with Todoist"
permalink: "/api-integration/todoist"
---

By the end of this guide, you will be able to use the [Todoist REST API](https://developer.todoist.com/rest/v1/#overview) to query tasks and projects from your Todoist account and generate a text report.

This guide assumes you have a Todoist account, and will walk you through the process of getting an API token and using that to make authenticated requests to the Todoist REST API. Having basic programming ability will be helpful for this guide.

#### What Is Useful About Integrating With Todoist

Although [Todoist has a rich set of features](https://todoist.com/features), it is only one part of what is often a suite of applications that one may use. Integrating with Todoist allows you to pull data from Todoist to populate elsewhere, and to push data into Todoist from another application. A wide variety of useful custom workflows can be implemented to integrate between different platforms.

#### Who Is This For

Although [Todoist provides some of their own integrations](https://todoist.com/integrations) and [some products offer their own integration services](https://ifttt.com/), there will always be custom workflows that one may want to implement, especially if between less popular or home grown applications.

For people with basic programming ability, they can build their own integrations with Todoist. Developers will primarily be the ones interested in this, however, even beginner developers learning to program can benefit by building something useful that will be impressive to potential employers.

#### Acquire API Token

The Todoist REST API uses the [Bearer HTTP Authentication Scheme](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#authentication_schemes). In order to make authenticated requests to Todoist, we will need an API token that was generated by your Todoist account.

Log into Todoist on your browser, and navigate to the Integrations page (if you are already logged in you can also just [click here](https://todoist.com/app/settings/integrations)).

![Acquire API Token]({{ site.baseurl }}{{ "/assets/img/todoist/1.png" }})

Scroll to the bottom of the page and copy the text under the API token field. Ensure that this text is kept secure and not shared publicly, as this can be used to freely control your Todoist account.

![Acquire API Token]({{ site.baseurl }}{{ "/assets/img/todoist/2.png" }})

#### Make Authenticated API Requests

Once you have your API token, you will be able to make authenticated requests to the Todoist REST API by providing an authorization header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) with your API token.

```
Authorization: Bearer $token
```

For example, [using curl](https://curl.se/), an authenticated API request to [get all active tasks](https://developer.todoist.com/rest/v1/#get-active-tasks) will look like the following:

```
$ curl -X GET \
  https://api.todoist.com/rest/v1/tasks \
  -H "Authorization: Bearer $token"
```


#### Get All Active Tasks

As we saw above, we are able to make a request to Todoist to get all active tasks for a user. The response from Todoist will be in the form of a JSON array, where each task is a JSON object:

```
[
    {
        "id": 2995104339,
        "project_id": 2203306141,
        "section_id": 7025,
        "parent_id": 2995104589,
        "content": "Buy Milk",
        "description": "",
        "comment_count": 10,
        "assignee": 2671142,
        "assigner": 2671362,
        "order": 1,
        "priority": 1,
        "url": "https://todoist.com/showTask?id=2995104339"
    },
    ...
]
```
