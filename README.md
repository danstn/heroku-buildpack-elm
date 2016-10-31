## Heroku Elm Buildpack

A simple buildpack that uses [npm's elm package](https://www.npmjs.com/package/elm) for binaries, and compiles `src/App.elm` to `public/app.js`.

### Configuration

1. Create a package.json (http://browsenpm.org/package.json) in your project root and add the `elm` dependency, i.e.

  ```
  {
    "name": "myapp",
    ...
    "dependencies": {
      "elm": "^0.17.1"
    }
  }
  ```

2. Add/modify `app.json` with the following buildpacks:

```
{
  "name": "myapp",
  "scripts": {},
  "env": {},
  "formation": {},
  "addons": [],
  "buildpacks": [
    { "url": "heroku/nodejs" },
    { "url": "https://github.com/supermario/heroku-buildpack-elm" }
  ]
}
```

3. :warning: Currently Heroku's multi-buildpack support uses the last buildpack for deployment, which means you need to have a buildpack loaded after this one, or a Procfile.

Here's a simple static server `Procfile`, assuming you've `npm install http-server --save`'ed to update your `package.json`.

```
web: http-server public/ -p $PORT --robots
```

Don't forget your `public/index.html`:

```
<!DOCTYPE HTML>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no, minimal-ui">
  <script src="app.js"></script>
</head>
<body>
  <script type="text/javascript">
    Elm.App.fullscreen()
  </script>
</body>
</html>
```
