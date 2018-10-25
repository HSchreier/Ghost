# Ghost publishing platform for Privatefunction.net


## Dev Commands
### Running Ghost

```
grunt dev
Default way of running Ghost in development mode
Builds admin files on start & then watches for changes
```
```
grunt dev --server
Ignores admin changes
```
```
grunt dev --no-server-watch
Ignores server changes
```
```
grunt build
Build admin client manually
```
```
grunt prod
Build full Ghost package for production
```

### Server Tests
Tests run with SQlite. To use MySQL, prepend commands with NODE_ENV=testing-mysql
```
grunt test-all
Run all tests
```
```
grunt test-unit
Run unit tests
```
```
grunt test-integration
Run integration tests
```
```
grunt test-functional
Run functional tests
```
```
grunt test:path/to/test.js
Run a single test
```
```
grunt lint
Make sure your code doesn't suck
```

###Client Tests
Client tests should always be run inside the core/client directory. Any time you have grunt dev running the client tests will be available at <http://localhost:4200/tests>


##Troubleshooting

Some common Ghost development problems and their solutions
ERROR: (EADDRINUSE) Cannot start Ghost
This error means that Ghost is already running, and you need to stop it

ERROR: ENOENT
This error means that the mentioned file doesn't exist

ERROR Error: Cannot find module
Install did not complete. Remove your node_modules and re-run yarn

Error: Cannot find module './build/default/DTraceProviderBindings'
You switched node versions. Remove your node_modules and re-run yarn

ENOENT: no such file or directory, stat 'path/to/favicon.ico' at Error (native)
Your admin client has not been built. Run grunt prod for production or grunt dev

TypeError: Cannot read property 'tagName' of undefined
You can't run ember test at the same time as grunt dev. Wait for tests to finish before continuing and wait for the "Build successful" message before loading admin.

yarn.lock conflicts
When rebasing a feature branch it's possible you'll get conflicts on yarn.lock because there were dependency changes in both master and <feature-branch>.

Note what dependencies have changed in package.json
(Eg. dev-1 was added and dev dep dev-2 was removed)
git reset HEAD package.json yarn.lock - unstages the files
git checkout -- package.json yarn.lock - removes local changes
yarn add dev-1 -D - re-adds the dependency and updates yarn.lock
yarn remove dev-2 - removes the dependency and updates yarn.lock
git add package.json yarn.lock - re-stage the changes
git rebase --continue - continue with the rebase

It's always more reliable to let yarn auto-generate the lockfile rather than trying to manually merge potentially incompatible changes.
