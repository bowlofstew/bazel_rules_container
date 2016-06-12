
<!---
Documentation generated by Skydoc
-->
<h1>Open Container Initiative Image Format support for Bazel</h1>


<nav class="toc">
  <h2>Rules</h2>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#container_image">container_image</a></li>
    <li><a href="#container_layer">container_layer</a></li>
  </ul>
</nav>
<hr>

<a name="overview"></a>
## Overview

These rules are used for building [OCI images](https://github.com/opencontainers/image-spec).

The `container_image` rule constructs a tarball which conforms to [v0.2.0](https://github.com/opencontainers/image-spec/blob/v0.2.0/serialization.md)
of the OCI Image Specification. Currently [Docker](https://docker.com) is the
only container runtime which is able to load these images.

Each image can contain multiple layers which can be created via the
`container_layer` rule.

<a name="container_image"></a>
## container_image

<pre>
container_image(<a href="#container_image.name">name</a>, <a href="#container_image.assemble_image">assemble_image</a>, <a href="#container_image.base">base</a>, <a href="#container_image.cmd">cmd</a>, <a href="#container_image.create_image">create_image</a>, <a href="#container_image.create_image_config">create_image_config</a>, <a href="#container_image.entrypoint">entrypoint</a>, <a href="#container_image.env">env</a>, <a href="#container_image.incremental_load_template">incremental_load_template</a>, <a href="#container_image.layers">layers</a>, <a href="#container_image.ports">ports</a>, <a href="#container_image.repository">repository</a>, <a href="#container_image.sha256">sha256</a>, <a href="#container_image.user">user</a>, <a href="#container_image.volumes">volumes</a>, <a href="#container_image.workdir">workdir</a>)
</pre>

Creates an image which conforms to the OCI Image Serialization specification.

More information on the specification is available at
https://github.com/opencontainers/image-spec/blob/v0.2.0/serialization.md.

By default this rule builds partial images which can be loaded into a container
runtime via `bazel run`. To build a standalone image build with .tar at the end
if the name. The resulting tarball is compatible with `docker load` and has the
structure:
```
{image-config-sha256}:
  {layer-sha256}.tar
{image-config-sha256}.json
...
manifest.json
```


<a name="container_image_outputs"></a>
### Outputs


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr>
      <td><code>%{name}.tar</code></td>
      <td>
        <p>A container image that contains all partial images which can be loaded
standalone by the container runtime.</p>
      </td>
    </tr>
    <tr>
      <td><code>%{name}.partial.tar</code></td>
      <td>
        <p>A partial container image that contains no parent images. Used when
running the rule to only load changed images into the container runtime.</p>
      </td>
    </tr>
  </tbody>
</table>

<a name="container_image_args"></a>
### Attributes


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="container_image.name">
      <td><code>name</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#name">Name</a>; Required</code></p>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr id="container_image.assemble_image">
      <td><code>assemble_image</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_image.base">
      <td><code>base</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>The base container image on top of which this image will built upon,
equivalent to FROM in a Dockerfile.</p>
      </td>
    </tr>
    <tr id="container_image.cmd">
      <td><code>cmd</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>A command to execute when the image is run.</p>
      </td>
    </tr>
    <tr id="container_image.create_image">
      <td><code>create_image</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_image.create_image_config">
      <td><code>create_image_config</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_image.entrypoint">
      <td><code>entrypoint</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>The entrypoint of the command when the image is run.</p>
      </td>
    </tr>
    <tr id="container_image.env">
      <td><code>env</code></td>
      <td>
        <p><code>Dictionary mapping strings to string; Optional</code></p>
        <p>Dictionary from environment variable names to their values when running
the container. <code>env = { "FOO": "bar", ... }</code></p>
      </td>
    </tr>
    <tr id="container_image.incremental_load_template">
      <td><code>incremental_load_template</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_image.layers">
      <td><code>layers</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>List of layers created by <code>container_layer</code> that make up this image.</p>
      </td>
    </tr>
    <tr id="container_image.ports">
      <td><code>ports</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>List of ports to expose.</p>
      </td>
    </tr>
    <tr id="container_image.repository">
      <td><code>repository</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>The repository for the default tag for the image. Images
generated are tagged by default to <code>bazel/package_name:target</code> for a
<code>container_image</code> target at <code>//package/name:target</code>. Setting this attribute
to <code>gcr.io/dummy</code> would set the default tag to
<code>gcr.io/dummy/package_name:target</code>.</p>
      </td>
    </tr>
    <tr id="container_image.sha256">
      <td><code>sha256</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_image.user">
      <td><code>user</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>The user that the image should run as. Because building the image never
happens inside a container, this user does not affect the other actions
(e.g., adding files).</p>
      </td>
    </tr>
    <tr id="container_image.volumes">
      <td><code>volumes</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>List of volumes to mount.</p>
      </td>
    </tr>
    <tr id="container_image.workdir">
      <td><code>workdir</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>Initial working directory when running the container. Because
building the image never happens inside a container, this working directory
does not affect the other actions (e.g., adding files).</p>
      </td>
    </tr>
  </tbody>
</table>

<a name="container_image_examples"></a>
### Examples

```python
load("@bazel_rules_container//container:container.bzl", "container_layer", "container_image")

container_layer(
    name = "jessie_layer",
    tars = [":jessie_tar"],
)
container_image(
    name = "jessie",
    layers = [":jessie_layer"],
)

# Using the `nodejs_files` layer from the `container_layer` example
container_image(
    name = "nodejs",
    layers = [":nodejs_files"],
)
```
<a name="container_layer"></a>
## container_layer

<pre>
container_layer(<a href="#container_layer.name">name</a>, <a href="#container_layer.build_layer">build_layer</a>, <a href="#container_layer.data_path">data_path</a>, <a href="#container_layer.debs">debs</a>, <a href="#container_layer.directory">directory</a>, <a href="#container_layer.files">files</a>, <a href="#container_layer.mode">mode</a>, <a href="#container_layer.sha256">sha256</a>, <a href="#container_layer.symlinks">symlinks</a>, <a href="#container_layer.tars">tars</a>)
</pre>

Create a tarball that can be used as a layer in a container image.


<a name="container_layer_outputs"></a>
### Outputs


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr>
      <td><code>%{name}.layer</code></td>
      <td>
        <p>The tarball that represents a container layer</p>
      </td>
    </tr>
  </tbody>
</table>

<a name="container_layer_args"></a>
### Attributes


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="container_layer.name">
      <td><code>name</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#name">Name</a>; Required</code></p>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr id="container_layer.build_layer">
      <td><code>build_layer</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_layer.data_path">
      <td><code>data_path</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>The directory structure from the files is preserved inside the
layer but a prefix path determined by <code>data_path</code> is removed from the
directory structure. This path can be absolute from the workspace root if
starting with a <code>/</code> or relative to the rule's directory. A relative path
may start with "./" (or be ".") but cannot go up with "..". By default, the
<code>data_path</code> attribute is unused and all files are supposed to have no
prefix.</p>
      </td>
    </tr>
    <tr id="container_layer.debs">
      <td><code>debs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>A list of Debian packages that will be extracted into the layer.</p>
      </td>
    </tr>
    <tr id="container_layer.directory">
      <td><code>directory</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>The directory in which to expand the specified files, defaulting
to '/'. Only makes sense accompanying one of files/tars/debs.</p>
      </td>
    </tr>
    <tr id="container_layer.files">
      <td><code>files</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>A list of files that should be included in the layer.</p>
      </td>
    </tr>
    <tr id="container_layer.mode">
      <td><code>mode</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>Set the mode of files added by the <code>files</code> attribute.</p>
      </td>
    </tr>
    <tr id="container_layer.sha256">
      <td><code>sha256</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>Internal attribute</p>
      </td>
    </tr>
    <tr id="container_layer.symlinks">
      <td><code>symlinks</code></td>
      <td>
        <p><code>Dictionary mapping strings to string; Optional</code></p>
        <p>Symlinks between files in the layer
<code>{ "/path/to/link": "/path/to/target" }</code></p>
      </td>
    </tr>
    <tr id="container_layer.tars">
      <td><code>tars</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>A list of tar files whose content should be in the layer.</p>
      </td>
    </tr>
  </tbody>
</table>

<a name="container_layer_examples"></a>
### Examples

```python
load("@bazel_rules_container//container:container.bzl", "container_layer")

filegroup(
    name = "nodejs_debs",
    srcs = [
        "nodejs.deb",
        "libgdbm3.deb",
        "perl.deb",
        "perl_modules.deb",
        "rlwrap.deb",
    ],
)

container_layer(
    name = "nodejs_files",
    debs = [":nodejs_debs"],
    symlinks = { "/usr/bin/node": "/usr/bin/nodejs" },
)
```