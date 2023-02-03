# Alt CMS

## Config API

### General structure

| Parameter    | Type              | Description |
|:-------------|:------------------|:------------|
| project      | Object            | An object that contains information about a project, including its name and URL.
| i18n | Object  | An object that contains information about the internationalization of a project.
| endUserAccounts | boolean | A boolean that determines if the CMS will have end user accounts. |
| email           | Object     | An object used for generating API endpoints to send form submissions to email (see more info below) |
| collections           | Object | Here you define the `<Collection>` items that will be included in the CMS. In every `<Collection>`, you specify the `<FieldItems>`, the return from the API is an array of `<Collection>` (see more below)|
| components | Object | Here you define the `<Component>` items that will be included in the CMS. The return from the API is an object `<Component>` |


### `email` Object
The following is the definition of the email object:
- `to`: Here is where you specify the email address that will receive messages from form submissions (a global email address for all forms)
- `endpoints`: Collection of endpoints for different forms in the project. Every entry in the object is an object with the following properties:
    - `subject`: The subject of the email
    - `to`: The email address that will receive the message (overrides the global email address)
    - `schema`: The schema of the form. This is an object with the following properties:
        - `name`: The name of the field
        - `type`: The type of the field (string or number)
        - `required`: A boolean that determines if the field is required
        

### `component` Object
Components are content-types that can manage only one entry. On the CMS they appear under the "Components" section.
To define a component you must create an object with the component name (that will be the endpoint in the API).
This object has these propreties:
- `name`: This is the name that will be shown on the CMS
- `schema`: This is the schema object where you define the fields of the current collection (see more below).
- `previewUri`: function with `id` as parameter that returns the preview URL of the collection item
- `endUserPermissions`: object representing if users that are not admin have write access to the component


### `collections` Object
Collections are content-types that can manage several entries. On the CMS they appear under the "Collections" section.
To define a collection you must create an object with the collecion name (that will be the endpoint in the API). 
This object has all the propreties of `component` plus these propreties: 
- `isHiddenInApi`: boolean representing if the collection is hidden when querying the API
- `isHiddenInList`: boolean representing if the collection is hidden from the list view
- `hasDraftPublish`: -- to be implemented --


### `schema` Object
To define a field in the `schema` object you must create an object with the field name as key (that will be the endpoint in the API).
Every field can have these props: 
- `name`: string representing the field name,
- `i18n`: boolean respresenting if the field is multilanguage
- `required`: boolean respresenting if this filed is required
- `hasListPreview`: boolean representing if the field is visible from the list view
- `isSearchable`: boolean representing if the item can be searched using the CMS's search functionality
- `isHiddenInApi`: boolean representing if the field is hidden when querying the API
- `notEditable`: boolean representing if the field is editable
- `unique`: boolean representing if the field must be unique
- `type`: string representing the field type (see below for more info)


### Field types
The `type` object have a main proprety that is `name` and can have other props depending on the type name. Here you can see the possible types and their props:
- `string`: generates input or textarea and has the next props:
  - `maxChars`: number representing the maximum number of characters. 
  - `validation`: string representing the validation type.

- `richText`: generates a rich text editor.

- `number`: generates an input of type number.


- `dropdown`: generates a dropdown and has the next props:
  - `items`: collection of objects. Each object must be named with a language code. The value of the object is an array of objects with the next props:
    - `value`: string representing the value of the dropdown item
    - `name`: string representing the label of the dropdown item


- `configurator`: generates a configurator and has the next props:
  - `enabledElements`: array of strings representing the enabled elements in the configurator

- `date`: generates a date picker.

- `color`: generates a color picker.

- `toggle`: generates a toggle and has the next props:
  - `default`: boolean representing the default value of the toggle

- `tags`: generates a tags input and has the next props:
    - `maxCount`: number representing the maximum number of tags


- `map`: generates a map and has the next props:
  - `center`: object with the next props:
    - `lat`: number representing the latitude of the center of the map
    - `lng`: number representing the longitude of the center of the map


- `component`: generates a component and has the next props:
  - `schemaFrom`: string representing the name of the component that will be used as schema
  - `schemaFromFieldName`: string representing the name of the field in the API
  - `referenceExisting`: boolean representing if the component can be referenced from an existing component or new one must be created

- `collection`: generates a collection and has the next props:
  - `schemaFrom`: string representing the name of the collection that will be used as schema
  - `schemaFromFieldName`: string representing the name of the field in the API
  - `referenceExisting`: boolean representing if the collection can be referenced from an existing collection or new one must be created

- `media`: generates a media upload component and has the next props:
  - `multiple`: boolean representing if the media component can have multiple files
  - `types`: array of strings representing the allowed media types

- `video`: generates a video link component and has the next props:
  - `provider`: string representing the video provider 



## CMS generation
- To change the CMS configuration, first stop the Docker container
- Make the necessary changes to the configuration file
- While the Docker container is down, run "docker-compose run cms npm run generate:prod" to generate the CMS with the new configuration
- Start the Docker container with "docker-compose up"
- Once the Docker container is running, run "docker-compose exec cms npm run db:migrate:create" to create a new migration
- When prompted, provide a meaningful name for the new migration
- Your configuration changes are now in effect
