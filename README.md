# add --color option to use color in non-tty terminal

# HAML-Lint

[![Gem Version](https://badge.fury.io/rb/haml-lint.svg)](http://badge.fury.io/rb/haml-lint)
[![Build Status](https://travis-ci.org/causes/haml-lint.svg)](https://travis-ci.org/causes/haml-lint)
[![Code Climate](https://codeclimate.com/github/causes/haml-lint.png)](https://codeclimate.com/github/causes/haml-lint)
[![Inline docs](http://inch-ci.org/github/causes/haml-lint.svg?branch=master)](http://inch-ci.org/github/causes/haml-lint)
[![Dependency Status](https://gemnasium.com/causes/haml-lint.svg)](https://gemnasium.com/causes/haml-lint)

`haml-lint` is a tool to help keep your [HAML](http://haml.info) files
clean and readable. In addition to HAML-specific style and lint checks, it
integrates with [RuboCop](https://github.com/bbatsov/rubocop) to bring its
powerful static analysis tools to your HAML documents.

You can run `haml-lint` manually from the command line, or integrate it into
your [SCM hooks](https://github.com/causes/overcommit). It uses rules
established by the team at [Causes.com](https://causes.com).

* [Requirements](#requirements)
* [Installation](#installation)
* [Usage](#usage)
* [Configuration](#configuration)
* [Linters](#linters)
* [Editor Integration](#editor-integration)
* [Git Integration](#git-integration)
* [Contributing](#contributing)
* [Changelog](#changelog)
* [License](#license)

## Requirements

 * Ruby 1.9.3+
 * HAML 4.0+

## Installation

```bash
gem install haml-lint
```

## Usage

Run `haml-lint` from the command line by passing in a directory (or multiple
directories) to recursively scan:

```bash
haml-lint app/views/
```

You can also specify a list of files explicitly:

```bash
haml-lint app/**/*.html.haml
```

`haml-lint` will output any problems with your HAML, including the offending
filename and line number.

Command Line Flag         | Description
--------------------------|----------------------------------------------------
`-c`/`--config`           | Specify which configuration file to use
`-e`/`--exclude`          | Exclude one or more files from being linted
`-i`/`--include-linter`   | Specify which linters you specifically want to run
`-x`/`--exclude-linter`   | Specify which linters you _don't_ want to run
`-h`/`--help`             | Show command line flag documentation
`--show-linters`          | Show all registered linters
`-v`/`--version`          | Show version

## Configuration

`haml-lint` will automatically recognize and load any file with the name
`.haml-lint.yml` as a configuration file. It loads the configuration based on
the directory `haml-lint` is being run from, ascending until a configuration
file is found. Any configuration loaded is automatically merged with the
default configuration (see `config/default.yml`).

Here's an example configuration file:

```yaml
linters:
  ImplicitDiv:
    enabled: false

  LineLength:
    max: 100
```

All linters have an `enabled` option which can be `true` or `false`, which
controls whether the linter is run, along with linter-specific options. The
defaults are defined in [`config/default.yml`](config/default.yml).

### Skipping Frontmatter

Some static blog generators such as [Jekyll](http://jekyllrb.com/) include
leading frontmatter to the template for their own tracking purposes.
`haml-lint` allows you to ignore these headers by specifying the
`skip_frontmatter` option in your `.haml-lint.yml` configuration:

```yaml
skip_frontmatter: true
```

## Linters

### [» Linters Documentation](lib/haml_lint/linter/README.md)

`haml-lint` is an opinionated tool that helps you enforce a consistent style in
your HAML files. As an opinionated tool, we've had to make calls about what we
think are the "best" style conventions, even when there are often reasonable
arguments for more than one possible style. While all of our choices have a
rational basis, we think that the opinions themselves are less important than
the fact that `haml-lint` provides us with an automated and low-cost means of
enforcing consistency.

## Editor Integration

### Vim

If you use `vim`, you can have `haml-lint` automatically run against your HAML
files after saving by using the
[Syntastic](https://github.com/scrooloose/syntastic) plugin. If you already
have the plugin, just add `let g:syntastic_haml_checkers = ['haml_lint']` to
your `.vimrc`.

### Sublime Text 3

If you use `SublimeLinter 3` with `Sublime Text 3` you can install the
[SublimeLinter-haml-lint](https://github.com/jeroenj/SublimeLinter-contrib-haml-lint)
plugin using [Package Control](https://sublime.wbond.net).

## Git Integration

If you'd like to integrate `haml-lint` into your Git workflow, check out our
Git hook manager, [overcommit](https://github.com/causes/overcommit).

## Contributing

We love getting feedback with or without pull requests. If you do add a new
feature, please add tests so that we can avoid breaking it in the future.

Speaking of tests, we use `rspec`, which can be run like so:

```bash
bundle exec rspec
```

## Changelog

If you're interested in seeing the changes and bug fixes between each version
of `haml-lint`, read the [HAML-Lint Changelog](CHANGELOG.md).

## License

This project is released under the MIT license.
