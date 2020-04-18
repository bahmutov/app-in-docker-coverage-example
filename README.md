# App in Docker, Cypress on Host Machine example

This example requires Docker.

1. Install dependencies
```shell
$ npm install
```
2. Start local application in local Docker container with
```shell
$ npm run docker:start
```

You will see it mapping the local folder into container-specific path `/var/to/my/app/e2e`
```text
-v $PWD:/var/to/my/app/e2e -w /var/to/my/app/e2e
```

The application runs on port `1234` and instruments all source files on the fly _with respect to Docker folder_ `/var/to/my/app/e2e`.

3. Run Cypress tests with
```shell
$ npm run cy:run
```

Tests execute, code coverage object is checked to see if the paths in `.nyc_output/out.json` exist locally. If not, it tries to automatically find how the current working folder matches to the Docker folder and files that `$PWD = /var/to/my/app/e2e`. You see it from the last debug messages

```text
  code-coverage found prefix that matches current folder: /var/to/my/app/e2e +0ms
  code-coverage found common folder /var/to/my/app/e2e that matches current working directory /Users/gleb/git/app-in-docker-coverage-example +0ms
  code-coverage replaced /var/to/my/app/e2e/app/main.js -> /Users/gleb/git/app-in-docker-coverage-example/app/main.js +0ms
  code-coverage replaced /var/to/my/app/e2e/app/second.js -> /Users/gleb/git/app-in-docker-coverage-example/app/second.js +0ms
  code-coverage saving updated file /Users/gleb/git/app-in-docker-coverage-example/.nyc_output/out.json +0ms
```

The report is then generated on the host machine and it has the right files.



