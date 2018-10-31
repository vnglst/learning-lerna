# Learning Lerna

clone repo

install dependencies with:

`yarn`

start app:

`yarn start`

Doesn't work! Packages not found. 💩

`npx lerna bootstrap`

Packages are symlinked. If you now run `yarn start` it should work. 🎉

But what now if you want to publish packages. For this your work has to be committed and pushed to a repo. Then you run:

`npx lerna publish`

Now all the packages that have updates will be published (in this case to npm). However if you now run `yarn start` it will still use the symlinked packages and not the published ones. What if you want to use the actual packages you published on npm?

For that you first make a small change in one of the dependencies, e.g. change 'alpha' to 'alpha2'. Then you run:

`npx lerna clean`

This will remove the symlinked dependencies. Then:

`npx lerna exec yarn`

This will do a yarn (install) in every package, which means that it will download the packages from npm instead of symlinking.

If, after having tested the actual npm packages, you want to return to the symlinked version you run `npx lerna clean` and then `npx lerna bootstrap` again.
