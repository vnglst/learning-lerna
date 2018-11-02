# Learning Lerna

## Symlinking packages

Clone this repo. Install dependencies:

```sh
yarn
```

Start app:

```sh
yarn start
```

Doesn't work! Packages not found. 💩

```sh
npx lerna bootstrap
```

Packages are symlinked. If you now run `yarn start` it should work. 🎉

## Publishing packages

But what if you want to publish packages? For this your work has to be committed and pushed to a repo. Then you run:

```sh
npx lerna publish
```

Now all the packages that have updates will be published (in this case to npm).

## Testing published packages

However if you now run `yarn start` it will still use the symlinked packages and not the published ones. What if you want to use the actual packages you published on npm? For that you first make a small test change in one of the dependencies, e.g. change 'alpha' to 'alpha2'. Then run:

```sh
npx lerna clean
```

This will remove the symlinked dependencies. Then:

```sh
npx lerna exec yarn
```

This will do a yarn (install) in every package, which means that it will download the packages from npm instead of symlinking.

If, after having tested the actual npm packages, you want to return to the symlinked version you run `npx lerna clean` and then `npx lerna bootstrap` again.

## Publishing updates

If you want to publish updates, you use the same command as before:

```sh
npx lerna publish # note: all changes have to be committed to git
```

Lerna will show you a dialog asking about the upgrade. By default Lerna will upgrade all packages to the same version number (kinda like you see when the React teams does an upgrade of both `React` and `ReactDOM`, those two are always on the exact same version).

So in our case, after this all packages will have `0.0.2` as a version number. As you will notice, Lerna also automatically updates any dependencies that packages might have on each other, so our `usage` package automatically upgrades to use version `0.0.2` of `alpha` and `beta`.

## Independent updates

If you don't want Lerna to automatically update all your packages to the same version number, you can set this in the `lerna.json` config file. Instead of using `version: "0.0.2"` you'd set it to `version: "independent"`.
