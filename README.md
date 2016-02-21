# php-crud-fields
Generic Field API for PHP7.
This library handles only the metadata about entities and fields related to them.


![Travis CI](https://travis-ci.org/back-2-95/php-crud-fields.svg?branch=master)

## TODO

I'll keep this todo list on top until the library is usable.

- Validate and force field data structure. Now they are just arrays of anything.
- In that structure, try to separate general, form and display related data.

## API

Create API and set storage:
```PHP
$api = new \BackTo95\Fields\Api();
$storage = new \BackTo95\Fields\Storage\FileStorage('data/entities');
$api->setStorage($storage);
```
Create EntityConfiguration with fields:
```PHP
$track_configuration = new \BackTo95\Fields\Entity\EntityConfiguration([
    'name' => 'track',
    'description' => 'Track represents musical track made with tracker software',
    'fields' => [
        'title' => [...],
        'description' => [...],
    ],
]);
```
Store the created EntityConfiguration:
```PHP
$api->storeEntityConfiguration($track_configuration);
```
Get stored EntityConfiguration by name:
```PHP
$api->getEntityConfiguration('track');
```

## EntityConfiguration data

Example entity: track (as in music)

````PHP
[
    'name' => 'track',
    'description' => 'Track represents musical track made with tracker software',
    'fields' => [
        'artist' => [
            'name' => 'artist',
            'widget' => 'text',
            'required' => 1,
        ],
        'title' => [
            'name' => 'title',
            'widget' => 'text',
            'required' => 1,
        ],
        'description' => [
            'name' => 'description',
            'widget' => 'textarea',
        ],
        'cover' => [
            'name' => 'cover',
            'widget' => 'image',
        ],
        'genre' => [
            'name' => 'genre',
            'widget' => 'tags',
            'required' => 1,
            'settings' => [
                'min' => 1
            ]
        ],
    ]
],
````

## Output

This library should just return entities and their field configurations which can be then used by some other component to store, render, validate etc.

## Rendering ##

Rendering is not responsibility of this class.

## UI for creating configurations ##

UI is not part of this library. It should be another library which requires and uses this library.

## Storage ##

Storing this configuration is not part of this library e.g. https://github.com/back-2-95/php-mongodb-crud

This library provides interface for Storage adapters and file based solution as an example.

By default this adapter uses path `data/entities` for storing configurations.
