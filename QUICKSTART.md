# PS SKU L3LS

## Quick start

In order to start you need python3.10+

### Build fabric

```bash
make build
```

or the faster version that skips doc generation:

```bash
make build-skip-docs
```

or the fastest version with pyavd:

```bash
make build-pyavd
```

#### Use a different AVD version

The default AVD version to build the project respects the choice done
while creating the project with
the [cookiecutter template](https://gitlab.aristanetworks.com:professional-services/ps-cookiecutter-avd-fabric).

You can change the AVD version by prepending your make commands with the variable
`AVD_VERSION=<your-version>`, for instance:

```shell
$> AVD_VERSION=4.8.0 make build
```

or by editing the AVD_VARIABLE in the [Makefile](Makefile)

#### Add a new AVD version

You can add new versions by creating new files under `.avd` with the filenames:

- requirements-<your-version>.txt: with the python requirements
- collection-requirements-<your-version>.yml: with the ansible collection requirements

These can be published AVD releases or development branches. See [.avd/requirements-devel.txt](.avd/requirements-devel.txt)
and [.avd/collection-requirements-devel.yml](.avd/collection-requirements-devel.yml) for an example usage for a branch.

#### Freezing requirements

In a production project is often a good idea to freeze your requirements to achieve deterministic builds, either between different
developers or inside CI environments. It's possible to freeze the project requirements with the make rule `freeze`. This will
generate the files `requirements.txt` and `collection-requirements.yml` in the project root. If these files are present they will
override the `AVD_VERSION` variable.

## Common issues on macOS

### Python version too old

Make sure your python version is 3.10 or newer.

### ansible galaxy collections download fails with an ssl error

Run the following command to update your certifi package with the newest CA bundle:

```shell
/Applications/Python\ 3.YOURVERSION/Install\ Certificates.command
```
