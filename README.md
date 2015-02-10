# Roger Style Guide

This is Digitpaint's Roger Style Guide.

1. [Release](#release)
    1. [Intern](#intern)
    1. [Version](#version)
    1. [Changelog](#changelog)
1. [Partials](#partials)
    1. [Loading partials](#loading-partials)
    1. [Define variables](#define-variables)
    1. [Inline use of variables](#inline-use-of-variables)

## Release

Every release should have it's own version number.
Add a git tag with the version number (eg. `v4.8.11`).
Futhermore the changelog has to be up-to-date.

### Intern

Also projects with both front- and back-end done by Digitpaint, should be release with an updated changelog and version tag.

### Version

Use Semantic Versioning, [SemVer](http://semver.org/).

Given a version number MAJOR.MINOR.PATCH, increment the:
1. MAJOR version when you make incompatible API changes,
1. MINOR version when you add functionality in a backwards-compatible manner, and
1. PATCH version when you make backwards-compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

### Changelog

- Update the changelog on development.

- Update version number if applicable.

- The most resent release is on top. Release date is added on release.
  ```
    Release: 1.0.1 (xx-xx-xxxx)
    -----------------------------

    * created detail page new design
    * added right info block to detail page
    ...

    Release: 1.0.0 (04-11-2013)
    -----------------------------

    * removed photo detail page
    ...
  ```

- Adding the changed files is optional for most projects, but required for some projects.

  __Note__: keep a consistent changelog.
  ```
    Release: 1.0.0 (08-11-2013)
    -----------------------------
    <!--- --
    A       /projecten/boekbaar-aanbod/holland/templates/detailpagina.html
    D       /projecten/boekbaar-aanbod/holland/templates/detailpagina-fotos.html
    M       /index.html
    ...
    -- --->

    * removed photo detail page
    * created detail page new design
    * added right info block to detail page
    ...
  ```

## Partials

### Loading partials

- Conform with the Ruby Style Guide.
  ```erb
    # bad
    <%=partial 'elements/save-bar' %>

    # good
    <%= partial 'elements/save-bar' %>
  ```

### Define variables

- At the top of the partial, all (config) variables should get a default.
  ```erb
    <%
      agenda_items = false if agenda_items.nil?
      group = true if group.nil?
      ...
    %>

    ...
  ```
  Conform with the Ruby Style Guide.
  ```erb
    # bad
    <%
    agenda_items = false if agenda_items.nil?
    group = true if group.nil?
    ...
    %>

    # bad
    <% agenda_items = false if agenda_items.nil? %>
    <% group = true if group.nil? %>
    ...
  ```

- Set the de default with:
  ```ruby
    # good
    agenda_items = false if agenda_items.nil?
  ```

  `if` is preferred, compared to `unless`
  ```ruby
    # bad
    agenda_items = false unless agenda_items.defined?

    # bad
    agenda_items = false unless agenda_items == true

    # bad
    agenda_items = false unless defined?(agenda_items)
  ```

  Conform with the Ruby Style Guide.

  > Use ||= freely to initialize variables.
  >
  > Don't use ||= to initialize boolean variables.

  ```ruby
    # bad
    agenda_items ||= false
  ```
  The following is devious:
  ```ruy
    # bad
    agenda_items = defined?(agenda_items) ? agenda_items : false
  ```

### Inline use of variables

- Variables are defined at the top of partial. Don't check for it!
  ```erb
    # good
    <% if with_image %>
      <span class="show-image"></span>
    <% end %>

    # bad
    <% if with_image == true %>
      <span class="show-image"></span>
    <% end %>

    # bad
    <% if defined?(with_image) && with_image != nil %>
      <span class="show-image"></span>
    <% end %>

    # bad
    <% if defined?(with_image) %>
      <span class="show-image"></span>
    <% end %>
  ```

