# strapi-portfolio

Stan's Strapi Portfolio

1. Create a new Strapi project

```
npx create-strapi-app my-project
```

2. Set up connection with Mongo DB

```
? Choose your installation type Custom (manual settings)
? Choose your default database client mongo
? Database name: strapi-portfolio
? Host: {MongoDB Atlas Host URL}
? +srv connection: true
? Port (It will be ignored if you enable +srv): 27017
? Username: stanlee
? Password: **********
? Authentication database (Maybe "admin" or blank):
? Enable SSL connection: Yes
```

3. Enter the newly created folder, and copy everything except README.md into the root folder

```
cd my-project
rsync -av --progress . .. --exclude README.md
```

4. After copying files, remove `my-project` folder

```
rm -rf my-project
```

5. Replace ./config/database.js into this one:

```
module.exports = ({ env }) => ({
  defaultConnection: 'default',
  connections: {
    default: {
      connector: 'mongoose',
      settings: {
        uri: env('DATABASE_URI'),
        srv: env.bool('DATABASE_SRV', true),
        port: env.int('DATABASE_PORT', 27017),
        database: env('DATABASE_NAME'),
      },
      options: {
        authenticationDatabase: env('AUTHENTICATION_DATABASE', null),
        ssl: env.bool('DATABASE_SSL', true),
      },
    },
  },
})
```

6. Copy all the files in `replace` folder into the root folder

```
cp -rf replace/.* .
```
