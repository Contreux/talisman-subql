### Talisman SubQL

The Talisman Subquery Repo allows us to retreive and analyse specific substrate events, blocks, and calls for analytics
and development purposes.

#### Environment

- [Typescript](https://www.typescriptlang.org/) are required to compile project and define types.

- Both SubQuery CLI and generated Project have dependencies and require [Node](https://nodejs.org/en/).

#### Install the SubQuery CLI

Install SubQuery CLI globally on your terminal by using Yarn or NPM:

```
npm install -g @subql/cli
yarn global add @subql/cli
```

Run help to see available commands and usage provide by CLI

```
subql help
```

## Initialize the Talisman repo

run following command to install all the dependencies of the repo.

```
yarn install
```

#### Code generation

In order to index the SubQuery project, and any changes made to it, it is mandatory to build the project.
Run this command under the project directory.

```
yarn codegen
```

## Build the project

In order to deploy the SubQuery project to the subquery hosted service, it is mandatory to pack the configuration before upload.
Run pack command from root directory of your project will automatically generate a `talisman-subql.tgz` file.

```
yarn build
```

## Indexing and Query

#### Run required systems in docker

Under the project directory run following command:

```
docker-compose pull && docker-compose up
or
yarn start:docker
```

#### Query the project

Open your browser and head to `http://localhost:3000`.

You should see a GraphQL playground showing in the explorer and the schemas that are ready to query.

For the `talisman-subql` project, try querying with the following code, then build more complex queries from there.

```graphql
{
  query {
    calls(
      filter: {
        section: { equalTo: "system" }
        method: { equalTo: "remarkWithEvent" }
        args: {
          contains: [
            {
              value: "0x54616c69736d616e202d20546865204a6f75726e657920426567696e73"
            }
          ]
        }
      }
    ) {
      nodes {
        id
        args
      }
    }
  }
}
```
