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
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
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
-d '{"title":"Episode title"}' http://www.example.com/loft/episode/2
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

`PUT http://www.example.com/loft/episode/`


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

## Get a specific Collection

```shell
curl "http://www.example.com/loft/collection/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Fresh Fruit #22 with Special Guest Father Figure and The Frosch Prince",
    "description": "The Frosch Prince returns for your 4 weekly dose of post punk,
    punk, rock, neo folk and pretty much anything else with six strings and a mic.",
    "segments": [
      {
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific collection

### HTTP Request

`GET http://www.example.com/loft/collection/<id>?include_broadcasts=true`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a Collection

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/collection/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint creates a collection.

### HTTP Request

`POST http://www.example.com/loft/collection/`

## Update a collection

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' \
http://www.example.com/loft/collection/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates a collection.

### HTTP Request

`PUT http://www.example.com/loft/collection/2`

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

## Get a specific Container

```shell
curl "http://www.example.com/loft/collection/<id>"
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Fresh Fruit #22 with Special Guest Father Figure and The Frosch Prince",
    "description": "The Frosch Prince returns for your 4 weekly dose of post punk,
    punk, rock, neo folk and pretty much anything else with six strings and a mic.",
    "segments": [
      {
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific collection

### HTTP Request

`GET http://www.example.com/loft/collection/<id>?include_broadcasts=true`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a Container

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/collection/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint creates a collection.

### HTTP Request

`POST http://www.example.com/loft/collection/`

## Update a container

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' \
http://www.example.com/loft/collection/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates a collection.

### HTTP Request

`PUT http://www.example.com/loft/collection/2`

## Delete a Specific Container



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

## Add Collection to a Container

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

## Remove collection from a Container



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


## Add Child container to container

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

## Remove child container from a Container



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




# Person

## Get a specific Person

```shell
curl "http://www.example.com/loft/person/<id>"
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
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific person

### HTTP Request

`GET http://www.example.com/loft/person/<id>?include_broadcasts=true`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a person

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


## Update a person

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' http://www.example.com/loft/episode/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates a person.

### HTTP Request

`PUT http://www.example.com/loft/person/`


## Delete a Person



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

This endpoint deletes a person.

### HTTP Request

`DELETE http://www.example.com/loft/person/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the person to delete













#Media

## Get a media item

```shell
curl "http://www.example.com/loft/media/<id>"
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
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific media item

### HTTP Request

`GET http://www.example.com/loft/person/<id>?include_broadcasts=true`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a media item

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/episode/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Media title",
    "description": "Media description",

  }

```

This endpoint creates media items.

### HTTP Request

`POST http://www.example.com/loft/media/`


## Update a media item

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' http://www.example.com/loft/media/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates media items.

### HTTP Request

`PUT http://www.example.com/loft/media/<id>`


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
ID | The ID of the person to delete








#Segment

## Get a segment

```shell
curl "http://www.example.com/loft/segment/<id>"
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
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific segment

### HTTP Request

`GET http://www.example.com/loft/segment/<id>`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a segment

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/episode/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Media title",
    "description": "Media description",

  }

```

This endpoint creates a segment.

### HTTP Request

`POST http://www.example.com/loft/media/`


## Update a segment

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' http://www.example.com/loft/media/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates a segment.

### HTTP Request

`PUT http://www.example.com/loft/segment/<id>`


## Delete a segment



```shell
curl "http://www.example.com/loft/segment/2"
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
curl "http://www.example.com/loft/broadcast/<id>"
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
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific broadcast

### HTTP Request

`GET http://www.example.com/loft/post/<id>`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a broadcast

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/episode/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Media title",
    "description": "Media description",

  }

```

This endpoint creates a post.

### HTTP Request

`POST http://www.example.com/loft/post/`


## Update a broadcast

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' http://www.example.com/loft/post/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates a broadcast.

### HTTP Request

`PUT http://www.example.com/loft/post/<id>`


## Delete a broadcast



```shell
curl "http://www.example.com/loft/post/2"
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
curl "http://www.example.com/loft/post/<id>"
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
        "title": "undefined",
        "media": {
          "mixcloud": "http://mixcloud.com/2352358",
          "mp4": "http://s3/2352358.mp4"
        }  
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
      "hosts":"The Frosch Prince"
    }
  }

```

This endpoint gets a specific segment

### HTTP Request

`GET http://www.example.com/loft/post/<id>`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_broadcasts | false | If set to true, the result will include broadcasts.

## Create a Post

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"title":"Episode title","description":"Episode description","meta":{"mixcloud"}}' \
http://www.example.com/loft/episode/
```

> The above command returns JSON structured like this:

```json

  {
    "id": 1,
    "title": "Media title",
    "description": "Media description",

  }

```

This endpoint creates a post.

### HTTP Request

`POST http://www.example.com/loft/post/`


## Update a post

```shell
curl -H "Content-Type: application/json" -X PUT \
-d '{"title":"Episode title"}' http://www.example.com/loft/post/2
```

> The above command returns JSON structured like this:

```json

  {
    "id": 2,
    "title": "Episode title",
    "description": "Episode description",

  }

```

This endpoint updates a post.

### HTTP Request

`PUT http://www.example.com/loft/post/<id>`


## Delete a post



```shell
curl "http://www.example.com/loft/post/2"
  -X DELETE
```



> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : true
}
```
