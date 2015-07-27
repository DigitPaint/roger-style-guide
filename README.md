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

Every release should have its own version number.
Add a git tag with the version number (eg. `v4.8.11`).
Futhermore, the changelog has to be up-to-date.

### Internal

Projects with both front- and back-end done by Digitpaint,
should be released with an updated changelog and version tag.

### Version

Use Semantic Versioning, [SemVer](http://semver.org/).

Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes,
1. MINOR version when you add functionality in a backwards-compatible manner, and
1. PATCH version when you make backwards-compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to
the MAJOR.MINOR.PATCH format.

### Changelog

- Update the changelog on development.

- Update version number if applicable.

- The most recent release is on top. Release date is added on release.
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

> Don't turn the mockup into an application.

- Keep the Ruby Style Guide in mind.

- Do not create partials with too many variables for configuration.

  Consider:

    - the necessity of the configuration
    - the alternative of a separate partial

- Also restrict the total number of variables within the partial.

### Loading partials

- Load partials in accordance with the Ruby Style Guide.
  ```erb
    # good
    <%= partial "elements/save-bar" %>

    # bad
    <%=partial "elements/save-bar" %>

    # bad
    <%= partial 'elements/save-bar' %>
  ```

### Define variables

- At the top of the partial, all (config) variables should get a default.
  ```erb
    # good
    <%
    with_image ||= false
    agenda_items ||= 5
    ...
    %>

    # bad
    <%
    with_image = false unless defined?(with_image)
    agenda_items = 5 unless defined?(agenda_items)
    ...
    %>

    # bad
    <% with_image = false unless defined?(with_image) %>
    <% agenda_items = 5 unless defined?(agenda_items) %>
    ...
  ```

- Set the default.
  ```ruby
    # good
    agendamage ||= false
    with_link ||= true
    agenda_items ||= 5
    
    # bad
    with_image = false unless defined?(with_image)
    with_link = true unless defined?(with_link)
    agenda_items = 5 unless defined?(agenda_items)

    # bad
    with_image = false unless with_image.defined?

    # bad
    with_image = false unless with_image == true

    # bad
    with_image = false if with_image.nil?

    # bad
    agenda_items = defined?(agenda_items) ? agenda_items : false
  ```

### Inline use of variables

- Variables are defined at the top of a partial. `defined?` etc. checks are
unnecessary.
  ```erb
    # good
    <% if with_image %>
      <span class="show-image"></span>
    <% end %>

    # good
    <% if agenda_items > 4 %>
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

