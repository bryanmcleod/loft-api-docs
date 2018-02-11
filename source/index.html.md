---
title: Loft API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:

includes:

search: true
---

# Introduction

This is the API Docs for Loft, a RESTful API for radio content management.


# Episode

An episode represents one discrete block of radio content. It has one or more segments which contain atomic audio media items. An episode may have one or more broadcasts (dated future or in the past). It has a meta object which contains an unstructured json object of any episodic metadata, for example hosts, guests or links. An episode always belongs to at least one collection.



## Get a specific Episode

```shell
curl "http://www.example.com/loft/episode/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Fresh Fruit #22 with Special Guest Father Figure and The Frosch Prince",
    "description": "The Frosch Prince returns for your 4 weekly dose of post punk, punk,
    rock, neo folk and pretty much anything else with six strings and a mic.",
    "segments": [
      {
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
      }
    ],
    "collections": [{
      "id": 4,
      "name":"episodes",
      "container": {
        "id":32,
        "name":"Fresh Fruit",
        "type":"show",
        "meta": {
          "hosts": ["The Frosch Prince"]
        }
      }
    },
    {

    }
    ],
    "broadcasts": [
      {
        "start_time":"2012-04-23T18:25:43.511Z",
       "end_time":"2012-04-23T20:25:43.511Z",
       "location":"Cashmere Loft",
       "original_broadcast":true
      },
      {
        "start_time":"2012-04-23T18:25:43.511Z",
       "end_time":"2012-04-23T20:25:43.511Z",
       "original_broadcast":false
      }
    ],
    "meta": {
      "hosts": ["The Frosch Prince"]
    }
  }

```

This endpoint gets a specific episode

### HTTP Request

`GET http://www.example.com/loft/episode/<id>?include_broadcasts=true`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create an Episode

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/episode/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint creates an episode.

### HTTP Request

`POST http://www.example.com/loft/episode/`


## Update an Episode

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Updated episode title"}' http://www.example.com/loft/episode/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates an episode.

### HTTP Request

`PATCH http://www.example.com/loft/episode/<id>`


## Delete a Specific Episode



```shell
curl "http://www.example.com/loft/episode/2"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```

This endpoint deletes an episode.

### HTTP Request

`DELETE http://www.example.com/loft/episode/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the episode to delete

# Collection

A collection is an ordered set of episodes. It may, for example, represent a playlist or a show's primary episode list. It always belongs to a container (A container could in turn be a show, or a special feature, ).

## Get a specific Collection

```shell
curl "http://www.example.com/loft/collection/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "name": "Bryan's playlist",
    "container": { }, //see container section for json structure
    "episodes": [...] //see episode section for json structure
  }

```

This endpoint gets a specific collection

### HTTP Request

`GET http://www.example.com/loft/collection/<id>`


## Create a Collection

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"name":"episodes","default_container_id":32}' \
http://www.example.com/loft/collection/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "name":"episodes",
    "default_container": { ... },
    "containers": [ ... ],
    "meta": {}
  }

```

This endpoint creates a collection.

### HTTP Request

`POST http://www.example.com/loft/collection/`

## Update a collection

```shell
curl -H "Content-Type: application/json" -X PATCH \
-d '{"name":"Bryans fav"}' \
http://www.example.com/loft/collection/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "name":"Bryans fav",
    "default_container_id": 32
  }

```

This endpoint updates a collection.

### HTTP Request

`PATCH http://www.example.com/loft/collection/2`

## Delete a Specific Collection



```shell
curl "http://www.example.com/loft/collection/2"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```

This endpoint deletes a collection.

### HTTP Request

`DELETE http://www.example.com/loft/collection/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the collection to delete

## Add Episode to Collection

```shell
curl -H "Content-Type: application/json" -X PUT -d '{"id":2}' http://www.example.com/loft/collection/2/episodes
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description"

  }

```

This endpoint adds an episode to a collection

### HTTP Request

`PUT http://www.example.com/loft/collection/2/episodes`

## Remove Episode from a Collection



```shell
curl "http://www.example.com/loft/collection/2/episodes/3"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 3,
  "removed" : true
}
```

This endpoint removes a listing of an episode in a collection

### HTTP Request

`DELETE http://www.example.com/loft/collection/<collection_id>/episodes/<episode_id>`

### URL Parameters

Parameter | Description
--------- | -----------
collection_id | The ID of the collection
episode_id | The ID of the episode



# Container

A container is a grouping concept that contains collections of episodes, posts and child containers. It could, for example represent a show, or a news page, or even a home page.

## Get a specific Container

```shell
curl "http://www.example.com/loft/collection/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "name":"Fresh Fruit",
    "type":"Show",
    "collections": [],
    "posts": [],
    "meta": {
      "host":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific collection

### HTTP Request

`GET http://www.example.com/loft/collection/<id>?include_broadcasts=true`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
posts_per_page | 10  | The number of posts per page
post_offset  | 0 |  The post the start
post_order_by  | "date"  |  The ordering attribute


## Create a Container

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"name":"Fresh Fruit","type":"Show"}' \
http://www.example.com/loft/collection/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "name": "Fresh Fruit",
    "type": "show"

  }

```

This endpoint creates a container.

### HTTP Request

`POST http://www.example.com/loft/container/`

## Update a container

```shell
curl -H "Content-Type: application/json" -X PATCH \
-d '{"name":"New Show Name"}' \
http://www.example.com/loft/container/1
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "name": "New Show Name",
    "type": "Show"

  }

```

This endpoint updates a container.

### HTTP Request

`PATCH http://www.example.com/loft/container/1`

## Delete a Specific Container



```shell
curl "http://www.example.com/loft/container/1"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "deleted" : true
}
```

This endpoint deletes a container.

### HTTP Request

`DELETE http://www.example.com/loft/container/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the container to delete

## Add Collection to a Container

```shell
curl -H "Content-Type: application/json" -X PUT -d '{"id":2}' http://www.example.com/loft/container/1/collections
```

> The above command returns JSON structured like this:

```json
{
"collections":[
    {
    "id": 1,
    "name":"episodes",
    "meta": {}
    }
  ]
}


```

This endpoint adds an collection to a container

### HTTP Request

`PUT http://www.example.com/containers/<container_id>/collections`

## Remove collection from a Container



```shell
curl "http://www.example.com/loft/containers/2/collections/3"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 3,
  "removed" : true
}
```

This endpoint removes a listing of a collection in a container

### HTTP Request

`DELETE http://www.example.com/loft/containers/<container_id>/collections/<collection_id>`

### URL Parameters

Parameter | Description
--------- | -----------
collection_id | The ID of the collection
episode_id | The ID of the episode


## Add child to container

```shell
curl -H "Content-Type: application/json" -X PUT -d '{"id":2}' http://www.example.com/loft/containers/1/children
```

> The above command returns JSON structured like this:

```json

{
  "children":[
  {
  "id": 1,
  "name": "Fresh Fruit",
  "type": "show"
  }]
}

```

This endpoint adds a child container to a container to allow you to create arbitrary container hierarchies

### HTTP Request

`PUT http://www.example.com/loft/containers/<parent_container_id>/children`

## Remove child from a Container



```shell
curl "http://www.example.com/loft/containers/3/children/3"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 3,
  "removed" : true
}
```

This endpoint removes a child container from a container, without deleting the child container itself.

### HTTP Request

`DELETE http://www.example.com/loft/container/<parent_container_id>/children/<child_id>`




# People

## Get a specific Person

```shell
curl "http://www.example.com/loft/people/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "name": "Frosch Prince",
    "meta": { ... }
  }

```

This endpoint gets a specific person

### HTTP Request

`GET http://www.example.com/loft/people/<id>`


## Create a person

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"name:"Frosch Prince"}' \
http://www.example.com/loft/people/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 4,
    "name": "Frosch Prince",
    "meta": {}
  }

```

This endpoint creates a person.

### HTTP Request

`POST http://www.example.com/loft/people/`


## Update a person

```shell
curl -H "Content-Type: application/json" -X PATCH \
-d '{"name":"Frosch Prince Jr."}' http://www.example.com/loft/people/4
```

> The above command returns JSON structured like this:

```json

  {
    "id": 4,
    "name": "Frosch Prince Jr.",
    "meta": {}
  }

```

This endpoint updates a person.

### HTTP Request

`PATCH http://www.example.com/loft/people/`


## Delete a Person



```shell
curl "http://www.example.com/loft/people/4"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 4,
  "deleted" : true
}
```

This endpoint deletes a person.

### HTTP Request

`DELETE http://www.example.com/loft/people/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the person to delete













#Media

A media item represents a single media file, for example an image or audio file.

## Get a media item

```shell
curl "http://www.example.com/loft/media/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "url": "http://s3.com/a.mp4",
    "type":"audio",
    "format": "MPEG-4",
  }

```

This endpoint gets a specific media item

### HTTP Request

`GET http://www.example.com/loft/media/<id>`


## Create a media item

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{  "url": "http://s3.com/a.mp4",\
  "type":"audio",\
  "format": "MPEG-4"}' \
http://www.example.com/loft/episode/
```

> The above command returns JSON structured like this:

```json

{
  "id": 1,
  "url": "http://s3.com/a.mp4",
  "type":"audio",
  "format": "MPEG-4",
}

```

This endpoint creates media items.

### HTTP Request

`POST http://www.example.com/loft/media/`




## Delete a Media Item



```shell
curl "http://www.example.com/loft/media/2"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```

This endpoint deletes a media item.

### HTTP Request

`DELETE http://www.example.com/loft/media/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the media item to delete








#Segment

A segment is a atomic part of an episode, with a single audio media file.

## Get a segment

```shell
curl "http://www.example.com/loft/segments/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "media_id": 4,
    "meta": {
      "guest":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific segment

### HTTP Request

`GET http://www.example.com/loft/segments/<id>`



## Create a segment

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"media_id":4 }' \
http://www.example.com/loft/segments/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "media_id": 4,
    "meta": {
      "guest":"The Frosch Prince"
    }
  }

```

This endpoint creates a segment.

### HTTP Request

`POST http://www.example.com/loft/segments/`


## Update a segment

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"media_id":"2"}' http://www.example.com/loft/segments/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "media_id": 2,
    "meta": {
      "guest":"The Frosch Prince"
    }
  }
```

This endpoint updates a segment.

### HTTP Request

`PATCH http://www.example.com/loft/segments/<id>`


## Delete a segment



```shell
curl "http://www.example.com/loft/segments/2"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```






#Broadcast

## Get a broadcast

```shell
curl "http://www.example.com/loft/broadcasts/<id>"
```

> The above command returns JSON structured like this:

```json

{
  "episode":{
    "id": 1,
    "title": "Fresh Fruit #22 with Special Guest Father Figure and The Frosch Prince",
  },
  "start_time":"2012-04-23T18:25:43.511Z",
  "end_time":"2012-04-23T20:25:43.511Z",
  "location":"Cashmere Loft",
  "original_broadcast":true
}

```

This endpoint gets a specific broadcast

### HTTP Request

`GET http://www.example.com/loft/broadcasts/<id>`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a broadcast

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{ \
  "episode_id: 4, \
  "start_time":"2012-04-23T18:25:43.511Z", \
  "end_time":"2012-04-23T20:25:43.511Z", \
  "location":"Cashmere Loft", \
  "original_broadcast":true \
}' \
http://www.example.com/loft/broadcasts/
```

> The above command returns JSON structured like this:

```json

{
  "episode":{
    "id": 1,
    "title": "Fresh Fruit #22 with Special Guest Father Figure and The Frosch Prince",
  },
  "start_time":"2012-04-23T18:25:43.511Z",
  "end_time":"2012-04-23T20:25:43.511Z",
  "location":"Cashmere Loft",
  "original_broadcast":true
}

```

This endpoint creates a broadcast.

### HTTP Request

`POST http://www.example.com/loft/broadcasts/`


## Update a broadcast

```shell
curl -H "Content-Type: application/json" -X PATCH \
-d '{"location":"HKW"}' http://www.example.com/loft/broadcasts/2
```

> The above command returns JSON structured like this:

```json

{
  "episode":{
    "id": 1,
    "title": "Fresh Fruit #22 with Special Guest Father Figure and The Frosch Prince",
  },
  "start_time":"2012-04-23T18:25:43.511Z",
  "end_time":"2012-04-23T20:25:43.511Z",
  "location":"Cashmere Loft",
  "original_broadcast":true
}
```

This endpoint updates a broadcast.

### HTTP Request

`PATCH http://www.example.com/loft/broadcasts/<id>`


## Delete a broadcast



```shell
curl "http://www.example.com/loft/broadcasts/2" \
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```














#Posts

## Get a post

```shell
curl "http://www.example.com/loft/posts/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "",
    "body":"",
    "meta": {
      "image_id":42
    }
  }

```

This endpoint gets a specific segment

### HTTP Request

`GET http://www.example.com/loft/posts/<id>`


## Create a Post

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Lorem ipsum dolor sit amet", \
"body":"consectetur adipiscing elit, sed do eiusmod tempor incididunt ut \
 labore et dolore magna aliqua. Ut enim ad minim veniam", \
 "meta":{"image_id":42}}' \
http://www.example.com/loft/posts/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
"title":"Lorem ipsum dolor sit amet",
"body":"consectetur adipiscing elit, sed do eiusmod tempor incididunt ut
labore et dolore magna aliqua. Ut enim ad minim veniam","meta":{"image_id":42}
  }

```

This endpoint creates a post.

### HTTP Request

`POST http://www.example.com/loft/posts/`


## Update a post

```shell
curl -H "Content-Type: application/json" -X PATCH \
-d '{"title":"New Title"}' http://www.example.com/loft/posts/2
```

> The above command returns JSON structured like this:

```json

{
  "id": 1,
"title":"New Title",
"body":"consectetur adipiscing elit, sed do eiusmod tempor incididunt ut
labore et dolore magna aliqua. Ut enim ad minim veniam","meta":{"image_id":42}
}

```

This endpoint updates a post.

### HTTP Request

`PATCH http://www.example.com/loft/posts/<id>`


## Delete a post



```shell
curl "http://www.example.com/loft/posts/2"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```
