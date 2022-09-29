- [Developer Guide](#developer-guide)
  - [Guides for Clients](#guides-for-clients)
  - [Auto Backports](#auto-backports)
  - [Compatibility Matrix](#compatibility-matrix)
  - [Getting Ready for Next Releases](#getting-ready-for-next-releases)
  - [Broken Links Checker](#broken-links-checker)
  - [Dependabot](#dependabot)

## Developer Guide

This developer guide includes useful steps to maintain the general health for clients and make them easier to develop and maintain.

### Guides for Clients

Add a `DEVELOPER_GUIDE` and `USER_GUIDE`/`GETTING_STARTED` to help developers and users work with clients.

See [opensearch-py](https://github.com/opensearch-project/opensearch-py) for more information.

### Auto Backports

Add an [auto backport workflow](https://github.com/opensearch-project/opensearch-java/blob/main/.github/workflows/backport.yml) to automatically backport pull requests to release branches. This alleviates the manual process of creating backport pull requests.

See [backports](WORKFLOWS.md#managing-backports) for more information.

### Compatibility Matrix

A compatibility matrix gives insight to the users and developers into what versions of the client are compatible with various versions of OpenSearch. To do so, add test support to run integration tests for the client across various versions of OpenSearch to determine compatibility.

See [integration workflow](https://github.com/opensearch-project/opensearch-java/blob/main/.github/workflows/test-integration.yml) and [COMPATIBILITY](https://github.com/opensearch-project/opensearch-java/blob/main/COMPATIBILITY.md) for more information.

### Getting Ready for Next Releases

Testing clients against unreleased changes of OpenSearch helps getting the clients ready for the next release and figuring out early if a certain change in OpenSearch has broken compatibility with clients.

See [unreleased integration](https://github.com/opensearch-project/opensearch-java/blob/main/.github/workflows/test-integration-unreleased.yml) for more information.

### Broken Links Checker

Create a Github Actions workflow to check for broken links in text files (.md, .html, .txt, .json) on pull requests and push. See [.github/workflows/links.yml](.github/workflows/links.yml) for an example.

See [lycheeverse/lychee-action](https://github.com/lycheeverse/lychee-action) for more information.

### Dependabot

Add [Dependabot configuration](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file) to the client repository to auto-update dependency versions for the package ecosystem.

See [dependabot.yml](https://github.com/opensearch-project/opensearch-java/blob/main/.github/dependabot.yml) for more information.