Ember Tools
-----------

![demo](http://cl.ly/image/2G0x323u150m/ember.gif)

## Installation

`npm install -g ember-tools`

## Features

- prescribed file organization for sanity
- scaffolding for learning curve mitigation
- template precompilation for performance
- single file application build for convenience
- generators for faster application development
- commonjs (node) style modules for js community &lt;3 and isolated testing

## Version Information

**Current Version: 0.2.0** (not backwards compatible with 0.1.*)

Package versions:

- ember v1.0.0-RC.5
- ember-data revision 12
- handlebars v1.0.0-rc.4
- jQuery 1.9.1

## Quickstart

```
npm install -g ember-tools
ember create my-app
cd my-app
ember generate --scaffold person name:string age:number
ember build
open js/index.html
# visit #/people
```

The first place to get started is configuring a route in
`config/routes.js` and then adding a template for the route.

## Usage

You can always run `ember --help` or `ember [command] --help` to get
usage information.

```
  Usage: ember [command] [options]

  Command-Specific Help

    ember [command] --help

  Commands:

    create                 creates a new ember application
    build                  compiles templates and builds the app
    generate [options]     generates application files
    precompile [options]   precompile templates from src dir to target dir

  Options:

    -h, --help     output usage information
    -V, --version  output the version number
```

## Guide

### Creating Stand-Alone Browser Apps

If you are creating a stand-alone browser application (no server, or
communication is through some api service) then use:

`ember create my-app`

- javascript assets created in `my-app/js`
- ember commands run from `my-app` root

Or if you already have the `my-app` directory, `cd` into it and call
ember create bare:

`ember create`

- javascript assets created in `./js`
- ember commands run from `./` root

There is nothing magical about the `index.html` file. Feel free to
replace it with your own (you probably should). Just make sure you
include a script tag pointing to `js/application.js`

### Creating Browser Apps as Part of Express or Rails (etc.)

If you are creating an ember app as part of a server-side framework like
express or ruby on rails use the `--js-path` option.

```sh
cd my-server-app
ember create --js-path public/javascripts
```

- javascript assets created in `my-server-app/public/javascripts`
- ember commands run from `my-server-app` root

Running `ember-build` will create a file at
`public/javascripts/application.js`. Require that in your server-app's
template, no other files are required.

### Building Your App

The build command pre-compiles all the templates to simple functions,
assigns all your modules to the `App` object based on their file names,
and then creates a single, concatenated file to be included in your app.

`ember build`

This build step makes adding new modules to your app as simple as
creating a file with the generate command. It will convert the file path
to an object, ie: `controllers/recipe -> App.RecipeController`,
`routes/recipes/index -> App.RecipesIndexRoute`.

If you want to inspect the objects being assigned to the `App` object
you can build without cleanup using the `--no-cleanup, -c` option and
then opening up the `index.js` file it creates:

`ember build -c`

You can also specify the path of the resulting application file to save
it somewhere other than the default path.

`ember build --out-file public/whatever.js`

### Building on File Changes

I like to use the `fs-monitor` npm module with this command to ignore
the intermediate files created by the build step:

`fsmonitor -p -d path/to/js '!index.js' '!templates.js' '!application.js' ember build`

### Scaffolding

I am not super proud of the scaffolding, but it gets your feet wet with
ember really quickly, so use it for fun, not profit :P

`ember generate --scaffold time_sheet description:string minutes:number`

### Generators

Ember tools provides generators for the different ember objects your app
will use. Basic usage is:

`ember generate [options] [name]`

So creating a recipe route would look like:

`ember generate --route recipe`

Or the shorter version:

`ember generate -r recipe`

If you have a route, you probably want a template too; you can combine
generator options:

`ember generate -rt recipe`

Below is a list of all generator commands the the files and objects they
create.

### Generator Examples

| options | object name | file |
| --------|-------------|------|
| `--model, -m burrito` | `Burrito` | `models/burrito.js` |
| `--view, -v burrito` | `BurritoView` | `views/burrito.js` |
| `--controller, -c post/comments` | `PostCommentsController` | `controllers/post/comments.js` |
| `--template, -t post/comments` | n/a | `templates/post/comments.handlebars` |
| `--route, -r taco_cart` | `TacoCartRoute` | `routes/taco_cart.js` |
| `--mixin, -x tacoable` | `Tacoable` | `mixins/tacoable.js` |
| `--helper, -l all_caps` | `allCaps` | `helpers/all_caps.js` |
| `-mvcrt tacos` | `Taco` <br>`TacosView` <br>`TacosController` <br>`TacosRoute` | `models/taco.js` <br>`views/tacos_view` <br>`controllers/tacos_controller.js` <br>`routes/taco_route.js` <br>`templates/tacos.handlebars`|

_Notes:_

- Models will always be singular.
- Sub-directories will be created for you if they don't exist.

### Precompiling Handlebars Templates for Ember

The build command already pre-compiles your templates, but you can use
the precompile command outside of the rest of ember-tools. To precompile
a bunch of templates found at `views/jst` to
`assets/javascripts/templates.js` run this command:

`ember precompile -d views/jst -f assets/javascripts/templates.js`

This will register each template on `Ember.TEMPLATES` with file paths
for keys.

## License and Copyright

[MIT Style License](http://opensource.org/licenses/MIT)

Copyright &copy; 2013 [Ryan Florence](http://ryanflorence.com)

## Contributing

Run tests with:

`npm test`

and the browser sanity tests:

`npm run-script browser`

Its usually easiest to create a branch and send a pull request against that branch instead of master. Single commits are preferred (no big deal though, I can squash and cherry-pick).

Thanks for using ember-tools!

