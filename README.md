# elm-to-pages 🌳
`elm-to-gh-pages` is an example of how to deploy an Elm app to GitHub pages using GitHub Actions. You can either copy this repo and start from their, or follow the explanation below to setup an existing project ⬇️.

## Usage
In a _public_ GitHub repo, go to `Settings > Pages > Source` and choose `GitHub Actions` instead of `Deploy from a branch`.

Now create a directory `.github/workflows/` and put [`elm-to-gh-pages.yml`](./.github/workflows/elm-to-gh-pages.yml) in it.

On your next push, after a few moments, your Elm app will be deployed to `yourusername.github.io/yourreponame`!

## Configuration

If you would like compile your app to JS instead of HTML, update the command in the `Build Elm artifact` section to `elm make src/Main.elm --output=main.js`. Make sure that you have an `index.html` file in your repo.

If your app does not use `Debug` and you would like the compiled code to be optimized, use `elm make src/Main.elm --output=main.js --optimize`.

To take it one step further, you can add the following block below the `Build Elm artifact step`.

```yaml
- name: Install uglify.js
  run: npm install uglify-js -g
- name: Uglify main.js
  run: uglifyjs main.js --compress "pure_funcs=[F2,F3,F4,F5,F6,F7,F8,F9,A2,A3,A4,A5,A6,A7,A8,A9],pure_getters,keep_fargs=false,unsafe_comps,unsafe" | uglifyjs --mangle --output main.js
```

## Contributing
Pull requests are welcome, especially if you have an idea on making this easier to use!