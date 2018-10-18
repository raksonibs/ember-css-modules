## 0.7.10 Super Scope (March 1, 2018)
### Fixed
- Support importing styles via `@value` and `composes:` from addons with `@scope`ed names.

## 0.7.9 Party Like It's 1992 (February 22, 2018)
### Fixed
- Ember 3.1 ships with a version of Glimmer that expects AST transforms to use [a singular `visitor` key rather than plural `visitors`](https://github.com/glimmerjs/glimmer-vm/pull/557). So we do that. Big thanks to [@luqman](https://github.com/luqman) for tracking this down.
- The internal computed property we set up to support `localClassNameBindings` now uses Ember's `defineProperty` for compatibility with the ES5 getters overhaul.

## ~0.7.8 Let's Pretend This Never Happened (February 22, 2018)~
### Changed
- Nothing. This was essentially a no-op republish of 0.7.7.

## 0.7.7 Prelease Blues (February 6, 2018)
### Fixed
- Prerelease versions of Ember CLI are correctly detected now.

## 0.7.6 Lint Roller (January 29, 2018)
### Added
- The plugin system now supports a notion of lint plugins, which will activate for developing addons even when they're in `devDependencies`.

## 0.7.5 Everything is Awesome (January 8, 2018)
### Fixed
- The `local-class` template transform should now play nicely with ember-font-awesome's own transforms (thanks [@buschtoens](https://github.com/buschtoens)!)
- The plugin registry no longer explodes when addons with no package keywords are present (thanks [@devotox](https://github.com/deotox)!)

## 0.7.4 String Theory (November 10, 2017)
### Added
- The ability to use `{{local-class}}` to inject classes from other modules is now public and documented (thanks [@kellyselden](https://github.com/kellyselden)!)

### Fixed
- `localClassNameBindings` now works with string values instead of just booleans (thanks [@luxferresum](https://github.com/luxferresum)!)
- `headerFiles` and `footerFiles` will now accept file paths with and without extensions
- Setup for `localClassNames` and `localClassNameBindings` now short circuits to avoid extra work for tagless components (thanks [@garno](https://github.com/garno)!)

## 0.7.3 After All (August 16, 2017)
### Added
- PostCSS plugins can now be specified to run against the final concatenated output of all modules using the `postprocess` array (thanks [@alexlafroscia](https://github.com/alexlafroscia)!)

### Fixed
- During testing, `import 'ember-css-modules/extensions'` is no longer required to have styles function correctly in integration tests.
- When no styles for a component can be found, `localClassNameBindings` now silently binds no classes instead of throwing an error.

## 0.7.2 Everything In Its Place (July 19, 2017)
### Added
- Modules to be included at the top or bottom of the concatenated output can now be set via the `headerModules` and `footerModules` configuration options. See the [module ordering guide](docs/ORDERING.md) for details.

### Changed
- `@after-module` has been deprecated in favor of the new `headerModules`/`footerModules` configuration

## 0.7.1 AST But Not Least (July 16, 2017)
### Added
- Support for Ember 2.15's new form factor for template AST transforms has been added.

### Fixed
- Styles resolution for components and controllers no longer assumes only a single `:` in container keys.

## 0.7.0 Plug It In (June 11, 2017)
### Added
- An initial cut of a plugin system has been implemented, allowing common PostCSS plugin sets, shared configuration, and other bits of reusable code to be packaged up and redistributed. See the README for a few implemented examples.

### Changed
- The CSS Modules pipeline has been upgraded and now uses PostCSS 6
- Some of the more advanced topics in the README have been broken out into dedicated mini-guides in an effort to keep the main document from being so overwhelming

### Fixed
- Attempting to pull styles from an addon that doesn't exist now provides a useful error message (#65).

## 0.7.0-beta.1 The Little Engine That Could (April 3, 2017)
### Changed
- There have been some internal changes to how styles are read from the app/addon trees. This should be a non-breaking change (and fixes a number of oddities, including previous incompatibility with lazy engines), but is enough of a shift to warrant a version bump and a note.
- Attempting to import a nonexistent `@value` or `compose` a nonexistent class is now a hard error at build time.

### Removed
- Support for the deprecated `styles` property has been removed.

## 0.6.5 Time Marches On (March 16, 2017)
### Fixed
- The (deprecated) computed `styles` property is no longer read-only, to allow for other component APIs that expect something with that name to be passed in.
- Avoid repurposing `this.options` in the addon to support Ember CLI 2.12 (#64)

## 0.6.4 RTFM (December 12, 2016)
### Fixed
- Now actually avoid triggering the ember-getowner-polyfill deprecation notice.

## 0.6.3 Fix It In Post (December 12, 2016)
### Added
- This addon will now run before ember-cli-postcss, enabling cooperative preprocessing as with ember-cli-sass and friends (#58).

### Fixed
- Upgraded ember-getowner-polyfill and eliminated a deprecation warning from its changed usage.

## 0.6.2 Nothing Comes from Nothing (November 30, 2016)
### Fixed
- Null local class values, e.g. `local-class={{if false 'foo'}}` no longer result in an exception (#57).

## 0.6.1 Hush Now (November 22, 2016)
### Fixed
- Removed a spurious warning when specifying a local-class for a component that doesn't yet have styles.

## 0.6.0 Helping Hand (November 6, 2016)
### Added
- Mirroring the `local-class` attribute, there is now a `local-class` helper that can be used in templates to reference local classnames e.g. when passing them to child components as properties.

### Deprecated
- In the past, attempting to import a nonexistent class or value would silently fail. This behavior is now deprecated and will be a hard error in the future.
- Usage of the `styles` computed property on components and controllers is now deprecated.
  - In templates, you can replace `{{styles.class-name}}` with `{{local-class 'class-name'}}`.
  - In JavaScript code, you can import the styles object via a normal ES2015 `import`.
  - As a migration stepping stone, you can import the styles object and set it on your component/controller's prototype to mimic the old form factor:
    ```js
    import styles from './styles';

    export default Ember.Component.extend({
      styles,

      // ...
    });
    ```

### Removed
- Support for Ember 1.13 has been removed; ember-css-modules now supports Ember 2.0+.

## 0.5.1 Cartography Edition (November 6, 2016)
### Added
- Source maps can now be generated for applications, with caveats. See the README and [ember-cli/broccoli-concat#58](https://github.com/ember-cli/broccoli-concat/issues/58) for details.
- A warning is now issued for addons that have no `addon/styles` directory, since Ember CLI won't invoke registered CSS preprocessors in that scenario.

### Fixed
- Fewer files are `require`d when ember-css-modules loads, lessening the overall impact it should have on Ember CLI's startup time

## 0.5.0 Window of Opportunity (September 26, 2016)
### Added
- Windows is now fully supported (#52).

### Fixed
- `localClassNameBindings` now works with classes that use `composes` (#48).

## 0.4.4 Virtually Indistinguishable (September 7, 2016)
### Added
- Virtual modules that export constants can be configured at build time.

### Fixed
- The configured modules extension can now contain a `.` (see #41 for history)

## 0.4.3 Change is the Only Constant (August 28, 2016)
### Added
- The `local-class` attribute now accepts dynamic values (#40)
- Components may specify `localClassNames` and `localClassNameBindings`, similar to `classNames` and `classNameBindings` respectively, to bind local classes to their root elements (#26)

### Fixed
- Values with commas and quotes can now be exposed in modules (#22)

## 0.4.2 A Certain Cachet (August 12, 2016)
### Added
- The beginnings of support for `@value` and `composes:` from addons, with some caveats. Real documentation forthcoming once the feature has a little time to bake.

### Fixed
- Provide caching information for `ember-cli-htmlbars` so it can correctly invalidate when the plugin changes.

## 0.4.1 Glimmer in the Eye (August 2, 2016)
### Added
- Preliminary support for Glimmer 2 with the Ember alpha series.

## 0.4.0 Think Locally (July 12, 2016)
### Added
- Local class names can be specified via the `local-class` attribute (#31)
- PostCSS options such as custom syntax are passed through via `postcssOptions` config (#34)
- The default extension for modules can be specified via `extension` config (#34)

### Fixed
- An `intermediateOutputPath` may be specified in order to have ember-css-modules emit to a location other than `<app-name>.css`, leaving other files in the styles tree untouched for further processing (#28). See the README for further details on how this in combination with the changes in #34 allow for working alongside other CSS preprocessors.

## 0.3.3 If At First (July 6, 2016)
### Fixed
- `_super` is now properly called in the addon `init()` to avoid a deprecation notice

## 0.3.2 Hidden Gems (May 1, 2016)
### Fixed
- Hidden files (e.g. `.DS_Store`) no longer break the build process (#21)

### Changed
- Final linking of `@value`s now occurs _before_ other PostCSS plugins execute (#23)

## 0.3.1 Contain Your Excitement (April 14, 2016)
### Fixed
- Classes named `container` can be used once again (#15)

## 0.3.0 Location, Location, Location (Mar 31, 2016)
### Changed
- Modules are now more intelligently ordered in the final output by default, according to composition and value dependencies. See the README for further details.

### Added
- Ability to override scoped name generation (#3)
- Greater (explicit) control over module ordering in final output (#7)

### Fixed
- Handle component lookup changes in Ember 2.5+ without crashing
- Pass through non-CSS files in the styles tree (#13)
- Don't rely on custom registry options set up in an initializer (#14)
