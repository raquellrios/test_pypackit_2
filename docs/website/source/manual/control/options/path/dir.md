# Directories

From the seven [main directories](/manual/fundamentals/structure/index.md) in your repository
that {{pp_meta.name}} manages and works with,
the [GitHub directory](/manual/fundamentals/structure/github.md)
and the [Docs directory](/manual/fundamentals/structure/docs.md)
have fixed paths according to GitHub requirements,
while the path to the other five directories can be customized.
As discussed before,
[Customizing the path to the control center directory](/manual/control/structure/index.md#location)
requires a configuration file outside the control center directory.
The path to the remaining four directories,
i.e., the [source](/manual/fundamentals/structure/source.md),
[tests](/manual/fundamentals/structure/tests.md),
[website](/manual/fundamentals/structure/website.md), and
[local](/manual/fundamentals/structure/local.md) directories,
along with the paths to subdirectories of the local directory,
can be customized using the `path.yaml` file
in your repository's control center, as described in this section.

## Setting
The `path.yaml` file accepts a key `dir`, where the value is an object with keys
`source`, `tests`, `website`, and `local`,
corresponding to the four main directories mentioned above.
The value of the `source`, `tests`, and `website` keys
must be a string representing the custom path to the corresponding directory,
relative to the root of the repository. The `local` key accepts an object with
keys `root`, `cache`, and `report`. The `root` key must be set to a string defining
the path to the local directory itself. The `cache` and `report` keys
correspond to the cache and report subdirectories of the local directory;
they accept an object with a key `root` that must be set to a string defining
the path to the corresponding subdirectory, relative to the root of the local directory.
In addition, they each define paths to other subdirectories of the corresponding cache/report subdirectory,
each used for a specific tool. By default, the following keys are defined
for both the `cache` and `report` subdirectories: `repodynamics`, `coverage`, `mypy`, `pylint`,
`pytest`, and `ruff`. Each of these keys must be set to a string defining the path
to the cache/report subdirectory for that tool,
relative to the root of the corresponding cache/report subdirectory.

::::{dropdown} Example

The default settings for the `local` key are as follows:

:::{code-block} yaml
:caption: 🗂 `path.yaml`
dir:
  local:
    root: .local
    cache:
      root: cache
      repodynamics: repodynamics
      coverage: coverage
      mypy: mypy
      pylint: pylint
      pytest: pytest
      ruff: ruff
    report:
      root: report
      repodynamics: repodynamics
      coverage: coverage
      mypy: mypy
      pylint: pylint
      pytest: pytest
      ruff: ruff
:::

This corresponds to the following directory structure for the local directory:

:::{code-block} text
📦 <REPOSITORY-ROOT>
 ┃
 ┗ 🗂 .local
   ┃
   ┣ 🗂 cache
   ┃ ┃
   ┃ ┣ 🗂 coverage
   ┃ ┃
   ┃ ┣ 🗂 mypy
   ┃ ┃
   ┃ ┣ 🗂 pylint
   ┃ ┃
   ┃ ┣ 🗂 pytest
   ┃ ┃
   ┃ ┣ 🗂 repodynamics
   ┃ ┃
   ┃ ┗ 🗂 ruff
   ┃
   ┗ 🗂 report
     ┃
     ┣ 🗂 coverage
     ┃
     ┣ 🗂 mypy
     ┃
     ┣ 🗂 pylint
     ┃
     ┣ 🗂 pytest
     ┃
     ┣ 🗂 repodynamics
     ┃
     ┗ 🗂 ruff
:::

::::

You can also add other custom keys under `dir.local.cache` and `dir.local.report`
for other tools that you use, and reference them in the corresponding configuration files.
Note that you do not have to specify all keys in the `path.yaml` file;
for all keys that are not specified, {{pp_meta.name}} will use the default values.
Also, you can entirely omit the `path.yaml` file if you do not want to customize any paths.

::::{dropdown} Example

For example, if you only want to
- change the path of the source directory to `my_source_directory`,
- change the path of the cache subdirectory to `my_cache_directory`, and
- add a new subdirectory `my_tool_subdirectory` under the report subdirectory
  for the tool `my_tool`,

then your `path.yaml` file should look like this:

:::{code-block} yaml
:caption: 🗂 `path.yaml`
dir:
  source: my_source_directory
  local:
    cache:
      root: my_cache_directory
    report:
      my_tool: my_tool
:::

::::


:::{admonition} Important Considerations
:class: important

- You must also manually create/rename/move the corresponding directories to match the set path,
  in the same commit where you create/modify/delete the `path.yaml` file.
- All four main directories must be orthogonal to all other
  [main directories](/manual/fundamentals/structure/index.md) in your repository,
  meaning that they cannot be a subdirectory of any other main directory.
:::


## Usage
{{pp_meta.name}} automatically manages a variety of files in your repository's main directories,
and performs a number of tasks that require access to these files.
For example, to run your tests and build your website, {{pp_meta.name}} needs to know
the path to tests and website directories. In addition, these paths are used as
substitutions in a number of other configuration files for your project,
so that you do not have to manually update these files when you change a path.
The following are just a few examples of configuration files where these paths are used:

:::{code-block} toml
:caption: 🗂 `package_python/build.toml`
[tool.setuptools.packages.find]
where = [ "${‎{ path.dir.source }}" ]

[tool.versioningit.onbuild]
source-file = "${‎{ path.dir.source }}/${‎{ package.name }}/__init__.py"
:::

:::{code-block} toml
:caption: 🗂 `package_python/tools/mypy.toml`
[tool.mypy]
cache_dir = "${‎{ path.dir.local.cache.mypy }}"
any_exprs_report = "${‎{ path.dir.local.report.mypy }}"
html_report = "${‎{ path.dir.local.report.mypy }}"
linecount_report = "${‎{ path.dir.local.report.mypy }}"
linecoverage_report = "${‎{ path.dir.local.report.mypy }}"
lineprecision_report = "${‎{ path.dir.local.report.mypy }}"
txt_report = "${‎{ path.dir.local.report.mypy }}"
:::


:::{code-block} toml
:caption: 🗂 `package_python/tools/ruff.toml`
[tool.ruff]
cache-dir = "${‎{ path.dir.local.cache.ruff }}"
:::

:::{code-block} yaml
:caption: 🗂 `ui/web.yaml`
readthedocs:
  conda:
    environment: ${‎{ path.dir.website }}/requirements.yaml
  sphinx:
    configuration: ${‎{ path.dir.website }}/source/conf.py
:::
