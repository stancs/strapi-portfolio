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

7. Run the Strapi CMS server in watch mode

```
npm run develop
```

8. If you want to add `content-export-import` plugin to import and export data, please refer to this: https://github.com/lazurey/strapi-plugin-content-export-import

This plugin is already added in this project

9. To host in Heroku, please read this guide:

https://strapi.io/documentation/developer-docs/latest/setup-deployment-guides/deployment/hosting-guides/heroku.html

Per this guide, please create a Heroku project `strapi-portfolio-stanlee`

```
heroku create strapi-portfolio-stanlee
```

10. To deploy, please run this command

```
> git push heroku HEAD:main
Enumerating objects: 172, done.
Counting objects: 100% (172/172), done.
Delta compression using up to 6 threads
Compressing objects: 100% (140/140), done.
Writing objects: 100% (172/172), 285.38 KiB | 8.65 MiB/s, done.
Total 172 (delta 29), reused 3 (delta 0), pack-reused 0
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Building on the Heroku-20 stack
remote: -----> Determining which buildpack to use for this app
remote: -----> Node.js app detected
remote:
remote: -----> Creating runtime environment
remote:
remote:        NPM_CONFIG_LOGLEVEL=error
remote:        USE_YARN_CACHE=true
remote:        NODE_VERBOSE=false
remote:        NODE_ENV=production
remote:        NODE_MODULES_CACHE=true
remote:
remote: -----> Installing binaries
remote:        engines.node (package.json):  >=10.16.0 <=14.x.x
remote:        engines.npm (package.json):   ^6.0.0
remote:        engines.yarn (package.json):  unspecified (use default)
remote:
remote:        Resolving node version >=10.16.0 <=14.x.x...
remote:        Downloading and installing node 14.17.0...
remote:        Bootstrapping npm ^6.0.0 (replacing 6.14.13)...
remote:        npm ^6.0.0 installed
remote:        Resolving yarn version 1.22.x...
remote:        Downloading and installing yarn (1.22.10)
remote:        Installed yarn 1.22.10
remote:
remote: -----> Installing dependencies
remote:        Installing node modules (yarn.lock)
remote:        yarn install v1.22.10
remote:        [1/4] Resolving packages...
remote:        [2/4] Fetching packages...
remote:        warning url-loader@1.1.2: Invalid bin field for "url-loader".
remote:        info fsevents@2.3.2: The platform "linux" is incompatible with this module.
remote:        info "fsevents@2.3.2" is an optional dependency and failed compatibility check. Excluding it from installation.
remote:        info fsevents@1.2.13: The platform "linux" is incompatible with this module.
remote:        info "fsevents@1.2.13" is an optional dependency and failed compatibility check. Excluding it from installation.
remote:        [3/4] Linking dependencies...
remote:        warning "strapi-admin > bootstrap@4.6.0" has unmet peer dependency "jquery@1.9.1 - 3".
remote:        warning "strapi-admin > bootstrap@4.6.0" has unmet peer dependency "popper.js@^1.16.1".
remote:        warning "strapi-plugin-users-permissions > grant-koa@5.4.8" has unmet peer dependency "koa@>=2.0.0".
remote:        [4/4] Building fresh packages...
remote:        Done in 97.45s.
remote:
remote: -----> Build
remote:        Running build (yarn)
remote:        yarn run v1.22.10
remote:        $ strapi build
remote:        Building your admin UI with production configuration ...
remote:        ℹ Compiling Webpack
remote:        ✔ Webpack: Compiled successfully in 1.76m
remote:        Done in 108.82s.
remote:
remote: -----> Pruning devDependencies
remote:        yarn install v1.22.10
remote:        [1/4] Resolving packages...
remote:        [2/4] Fetching packages...
remote:        info fsevents@2.3.2: The platform "linux" is incompatible with this module.
remote:        info "fsevents@2.3.2" is an optional dependency and failed compatibility check. Excluding it from installation.
remote:        info fsevents@1.2.13: The platform "linux" is incompatible with this module.
remote:        info "fsevents@1.2.13" is an optional dependency and failed compatibility check. Excluding it from installation.
remote:        [3/4] Linking dependencies...
remote:        warning "strapi-admin > bootstrap@4.6.0" has unmet peer dependency "jquery@1.9.1 - 3".
remote:        warning "strapi-admin > bootstrap@4.6.0" has unmet peer dependency "popper.js@^1.16.1".
remote:        warning "strapi-plugin-users-permissions > grant-koa@5.4.8" has unmet peer dependency "koa@>=2.0.0".
remote:        [4/4] Building fresh packages...
remote:        warning Ignored scripts due to flag.
remote:        Done in 11.73s.
remote:
remote: -----> Caching build
remote:        - yarn cache
remote:
remote: -----> Build succeeded!
remote:  !     Unmet dependencies don't fail yarn install but may cause runtime issues
remote:        https://github.com/npm/npm/issues/7494
remote:
remote: -----> Discovering process types
remote:        Procfile declares types     -> (none)
remote:        Default types for buildpack -> web
remote:
remote: -----> Compressing...
remote:        Done: 132.4M
remote: -----> Launching...
remote:        Released v3
remote:        https://strapi-portfolio-stanlee.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/strapi-portfolio-stanlee.git
 * [new branch]      HEAD -> main
```

11. You can open your project using the command line:

```
heroku open
```

12. In Heroku setting, you will need to set these `Config Vars`:

```
HOST
PORT
DATABASE_URI
DATABASE_NAME
```

13. You can setup Strapi in this URL:

https://strapi-portfolio-stanlee.herokuapp.com/admin
