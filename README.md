# depcheck-safe
Like depcheck but checks if removing the packages will cause the build to break, rolling back if so.

This (will be) an npm package which uses `depcheck` to determine which dependencies are not needed, then goes through those dependencies and removes them one by one. If removing one causes the build or tests to break, it will be rolled back, and another package will be removed until all reported unused dependencies have been processed. While not perfect, it reduces the number of false positives which can be manually reviewed.

## I have to have this now I can't wait

Run:

`npm -g install depcheck`

`depcheck > depcheck.txt`

Remove all asterixis and headings in the `depcheck.txt` file. Place in root folder of nodejs project.

There is a proof of concept called `depcheck-safe.bat` which can be placed in the root of the nodejs project, and then run using command prompt. Warning: it will overwrite the `package.json` file, so make a backup first, and ensure that no modules have been installed using `-g` to get best results.

It will systematically build, test, lint, and e2e test the project. If any step fails, it will re-install the previously removed package, and go to the next one. When finished, `package.json` won't have any packages that were flagged by `depcheck`, removed, and passed all tests and builds.
