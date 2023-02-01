# Alt CMS

## Config API

### General structure

| Parameter    | Type              | Description |
|:-------------|:------------------|:------------|
| project      | Object            | An object that contains information about a project, including its name and URL. The object has two properties: `<name: string>`: represents the name of the project. `<url: string>`: represents the URL associated with the project. |
| i18n | Object  | An object that contains information about the internationalization of a project. This object has one property `<locales>` which is an array of objects, each representing a language. Each language object has two properties: `<name: string>`: represents the name of the language. `<code: string>`: a string that represents the code for the language. |
| email           | Object     | An object used for generating API endpoints to send form submissions to email (see more info below) |
| collections           | Object | Here you define the `<Collection>` items that will be included in the CMS. In every `<Collection>`, you specify the `<FieldItems>`, the return from the API is an array of `<Collection>` (see more below)|
| components | Object | Here you define the `<Component>` items that will be included in the CMS. The return from the API is an object `<Component>` |


### `<email>` Object
The following is the definition of the email object:
- `<to>: string` `<required>`: Here is where you specify the email address that will receive messages from form submissions (a global email address for all forms)
- `<endpoints: (property) endpoints: { [endpoint: string]: MailEndpoint>}`: Here is where you specify the endpoints needed for the project. Here is the structure:
{% capture some_var %}
{% highlight some_language linenos %}
[endpoint: string]: {
    subject: string,
    schema: {
        [key: string]: {
            name: string,
            type: string | number,
            reqired: string | undefined
        }
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=some_var %}




## CMS generation
- To change the CMS configuration, first stop the Docker container
- Make the necessary changes to the configuration file
- While the Docker container is down, run "docker-compose run cms npm run generate:prod" to generate the CMS or apply the new changes
- Start the Docker container with "docker-compose up"
- Once the Docker container is running, run "docker-compose exec cms npm run db:migrate:create" to create a new migration
- When prompted, provide a meaningful name for the new migration
- Your configuration changes are now in effect
