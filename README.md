## Heroku Elm Buildpack

A simple buildpack that uses [npm's elm package](https://www.npmjs.com/package/elm) for binaries, and compiles `elm/src/Main.elm` to `public/main.js`.

:warning: Currently Heroku's multi-buildpack support uses the last buildpack for deployment, which means you need to have a buildpack loaded after this one.

### Configuration

1. Create a package.json (http://browsenpm.org/package.json) in your project root and add the `elm` dependency, i.e.

  ```
  {
    "name": "myproject",
    ...
    "dependencies": {
      "elm": "^0.17.1"
    }
  }
  ```

2. Add the buildpacks in order. For example, a Rails application with Elm:

  ```
  # Add buildpacks
  $ heroku buildpacks:add heroku/nodejs
  $ heroku buildpacks:add https://github.com/supermario/heroku-buildpack-elm
  $ heroku buildpacks:add heroku/ruby

  # List buildpacks to check ordering
  $ heroku buildpacks
  === Buildpack URLs
  1. heroku/nodejs
  2. https://github.com/supermario/heroku-buildpack-elm
  3. heroku/ruby
  ```
