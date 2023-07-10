[![Gluon](.github/assets/gluon_logo.svg)](https://gluonhq.com)

[![License](https://img.shields.io/github/license/gluonhq/emoji)](https://opensource.org/licenses/GPL-3.0)

# Reusable workflows for Github Action

Contains reusable workflows which can be used across projects to ease release of projects under the Gluon umbrella.

## Workflows

### maven-pre-release

Updates Maven project version with the release version by removing `-SNAPSHOT` from the project's `pom.xml`.
It commits back the `pom.xml` to the repository with a commit `Release vX.X.X` and tags the commit with `X.X.X`.

#### Inputs

| Input        | Default           | Description                                                                                                |
|--------------|-------------------|------------------------------------------------------------------------------------------------------------|
| buildDir     | current directory | Maven build directory                                                                                      |
| depProperty  |                   | Property name to be updated with new release version. Mostly used in samples projects.                     |
| depDirectory |                   | project directory containing the pom.xml to be updated with new release version i.e. samples project path. |

#### Outputs

| Output | Default | Description                    |
|--------|---------|--------------------------------|
| tag    |         | Release version of the project |


### maven-post-release

Does the following:
* Creates a Github release with release notes
* Updates Maven project version with the next development version.
The next development version can be passed to the workflow explicitly.
Otherwise, it will be calculated by incrementing the minor version the project version.
It then adds `-SNAPSHOT` to the next development version.
It commits back the `pom.xml` to the repository with a commit `Prepare development of X.X.X`.
* If both `depProperty` and `depDirectory` is provided, then it will also increment the dependency to the next development version.

#### Inputs

| Input        | Default                 | Description                                                                                                |
|--------------|-------------------------|------------------------------------------------------------------------------------------------------------|
| nextVersion  | calculated from pom.xml | Next development version without "SNAPSHOT"                                                                |
| buildDir     | current directory       | Maven build directory                                                                                      |
| depProperty  |                         | Property name to be updated with new release version. Mostly used in samples projects.                     |
| depDirectory |                         | project directory containing the pom.xml to be updated with new release version i.e. samples project path. |
| tag          |                         | release tag to checkout                                                                                    |
