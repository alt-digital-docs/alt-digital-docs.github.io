# Alt CMS

### Config API

#### Structure

| Parameter    | Type              | Description |
|:-------------|:------------------|:------------|
| project      | Object            | An object that contains information about a project, including its name and URL. The object has two properties: name: a string that represents the name of the project. url: a string that represents the URL associated with the project. |
| out of stock | good and plenty   | nice        |
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
