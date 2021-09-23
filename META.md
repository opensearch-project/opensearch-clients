- [Managing OpenSearch Clients](#managing-opensearch-clients)
  - [Install GH](#install-gh)
  - [Install Meta](#install-meta)
  - [Check Out Clients](#check-out-clients)
  - [Get Repo Info](#get-repo-info)
  - [Add a New Client](#add-a-new-client)
  - [Create or Update Labels in All Client Repos](#create-or-update-labels-in-all-client-repos)
  - [Create an Issue in All Client Repos](#create-an-issue-in-all-client-repos)
  - [Open a Pull Request in Each Repo](#open-a-pull-request-in-each-repo)

## Managing OpenSearch Clients

We use [meta](https://github.com/mateodelnorte/meta) to manage OpenSearch clients as a set.

### Install GH

Install and configure GitHub CLI from [cli.github.com/manual/installation](https://cli.github.com/manual/installation). Authenticate with `gh auth login` and ensure that it works, e.g. `gh issue list`.

### Install Meta

```sh
npm install -g meta
```

### Check Out Clients

```sh
cd clients
meta git update
```

Use `meta git pull` to subsequently pull the latest revisions.

### Get Repo Info

```sh
clients> meta gh issue list
```

### Add a New Client

```sh
cd clients
meta project import opensearch-new-client git@github.com:opensearch-project/opensearch-new-client.git
```

### Create or Update Labels in All Client Repos

Install [ghi](https://github.com/stephencelis/ghi), e.g. `brew install ghi`.

```
meta exec "ghi label 'backwards-compatibility' -c '#773AA8'
```

This makes it easy to create version labels.

```
meta exec "ghi label 'untriaged' -c '#fbca04'"
meta exec "ghi label 'v1.0.0' -c '#d4c5f9'"
meta exec "ghi label 'v1.1.0' -c '#c5def5'"
meta exec "ghi label 'v2.0.0' -c '#b94c47'"
```

### Create an Issue in All Client Repos

Create a file for the issue body, e.g. `issue.md`.

```
meta exec "gh issue create --label backwards-compatibility --title 'Ensure backwards compatibility with ODFE' --body-file ../issue.md"
```

### Open a Pull Request in Each Repo

In [opensearch-build#497](https://github.com/opensearch-project/opensearch-build/issues/497) we needed to remove `integtest.sh` from each repo.

We'll be pushing to forks. Make sure to replace `username` with your GitHub username below and to fork all the repos first.

```
meta exec "gh repo fork"
```

Ensure that a remote is setup for each client pointing to our forks.

```
meta exec "git remote get-url origin | sed s/opensearch-project/username/g | xargs git remote add username"
```

Remove a file, e.g. `integtest.sh`, commit and push.

```
meta exec "git rm integtest.sh"
meta exec "git add --all"
meta exec "git checkout -b remove-integtest-sh"
meta exec "git commit -s -m 'Removed integtest.sh.'"
meta exec "git push username remove-integtest-sh"
meta exec "gh pr create --title 'Removing default integtest.sh.' --body='Coming from https://github.com/opensearch-project/opensearch-build/issues/497, removing default integtest.sh.'"
```
