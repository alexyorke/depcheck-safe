# depcheck-safe
Like depcheck but checks if removing the packages will cause the build to break, rolling back if so.

This (will be) an npm package which uses `depcheck` to determine which dependencies are not needed, then goes through those dependencies and removes them one by one. If removing one causes the build or tests to break, it will be rolled back, and another package will be removed until all reported unused dependencies have been processed. While not perfect, it reduces the number of false positives.
