# Alt CMS

### Config API

#### Structure

| Parameter    | Type              | Description |
|:-------------|:------------------|:------------|
| project      | Object            | An object that contains information about a project, including its name and URL. The object has two properties: `<name: string>`: represents the name of the project. `<url: string>`: represents the URL associated with the project. |
| i18n | Object  | An object that contains information about the internationalization of a project. This object has one property `<locales>` which is an array of objects, each representing a language. Each language object has two properties: {% `<name: string>`: represents the name of the language. %} {% `<code: string>`: a string that represents the code for the language. %} |
| ok           | good `oreos`      | hmm         |
| ok           | good `zoute` drop | yumm        |

### CMS generation
- To change the CMS configuration, first stop the Docker container
- Make the necessary changes to the configuration file
- While the Docker container is down, run "docker-compose run cms npm run generate:prod" to generate the CMS or apply the new changes
- Start the Docker container with "docker-compose up"
- Once the Docker container is running, run "docker-compose exec cms npm run db:migrate:create" to create a new migration
- When prompted, provide a meaningful name for the new migration
- Your configuration changes are now in effect
