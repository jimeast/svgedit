# Creating a new svg-edit release

## Prepare

1. `npm test` - Ensure build steps occur and tests are passing
1. `npm run build-doc` - Ensure JSDoc can build and is available for site build
1. `npm run grep-doc` - For JSDoc, we ensure that a minimum of generic types
    have been added (e.g., "number" should instead be "Float" or "Array",
    and "object", "function", or "array" should be replaced by more specific
    `@interface`s, `@typdef`s, or `@callback`. Deriving types can use
    `PlainObject` or `GenericArray` to indicate the simple base type was
    intentional. `*` should also be checked. The script reports all failing
    matches within `editor`. There should be none.
1. Preview which files will be included once published (taking into
    account `.npmignore`), by using `npm pack` (taking care to remove
    the `.tgz` tarball file that it creates).

## Update the main project
<!--
1. Update the VERSION variable in Makefile.
-->
1. Update `version` in `package.json` (and `package-lock.json` (via `npm i`)).
1. Update the CHANGES file with a summary of all changes.
1. Add new release info to `Recent news` section in README
1. Commit these changes
<!-- with `git commit -m "Updating Makefile and CHANGES for release X.Y.Z"`-->.
1. Tag the version, prefixed by "v", e.g., `v3.0.1`.

The above steps can be done on a fork and committed via a pull request.

## Create the release on `gh-pages`
<!--
2. From the root directory run `make`.
3. Copy `build/svg-edit-X.Y.Z/`, `build/svg-edit-X.Y.Z-src.tar.gz`, and `build/svg-edit-X.Y.Z.zip` to a temporary directory.
-->

1. Ensure you are on the `master` branch with `git checkout master`.
1. Switch to the `gh-pages` branch with `git checkout gh-pages`.
1. Run the `build.js` executable (`npm run build` if within the project root
    directory).
1. Commit these changes with `git commit -m "Updating files for release X.Y.Z"`.
1. Switch back to the `master` branch with `git checkout master`.
1. Ensure this step worked by visiting
    <https://svg-edit.github.io/svgedit/releases/svg-edit-X.Y.Z/editor/svg-editor.html>
    (and in an ES6-Module-compliant browser,
    <https://svg-edit.github.io/svgedit/releases/svg-edit-X.Y.Z/editor/svg-editor-es.html>).

The above steps can be done on a fork and committed via a pull request.

## Create the release on GitHub
<!--
4. Attach the `svg-edit-X.Y.Z-src.tar.gz` and `build/svg-edit-X.Y.Z.zip` files to the release.
-->
1. Go to <https://github.com/SVG-Edit/svgedit/releases> and select
  `Draft a new release`.
1. Make the release target point at the commit where the <!-- makefile and -->
  changes were updated.
1. Write a short description of the release and include a link to the live
  version:
  <https://svg-edit.github.io/svgedit/releases/svg-edit-X.Y.Z/editor/svg-editor.html>.
  See the previous releases for the format.
1. Create the release!

You will need to be a member of the SVG-Edit GitHub group to do this step.

## Publish to npm

1. `npm publish`
