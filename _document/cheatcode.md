# GITHUB CLI

- [GITHUB CLI](#github-cli)
  - [`gh auth`](#gh-auth)
    - [`gh auth login [flags]`](#gh-auth-login-flags)
    - [`gh auth logout`](#gh-auth-logout)
    - [`gh auth refresh [flags]`](#gh-auth-refresh-flags)
    - [`gh auth setup-git [flags]`](#gh-auth-setup-git-flags)
    - [`gh auth status [flags]`](#gh-auth-status-flags)
    - [`gh auth token [flags]`](#gh-auth-token-flags)
  - [`gh repo`](#gh-repo)
    - [Repository Fields](#repository-fields)
    - [`gh repo create [<name>] [flags]`](#gh-repo-create-name-flags)
    - [`gh repo list [<owner>] [flags]`](#gh-repo-list-owner-flags)
    - [`gh repo rename <new-name> [flags]`](#gh-repo-rename-new-name-flags)
    - [`gh repo view <repository> [flags]`](#gh-repo-view-repository-flags)
    - [`gh repo archive <repository> [flags]`](#gh-repo-archive-repository-flags)
    - [`gh repo clone  [<directory>] [-- <gitflags>...]`](#gh-repo-clone--directory----gitflags)
    - [`gh repo delete`](#gh-repo-delete)
    - [`gh repo edit [<repository>] [flags]`](#gh-repo-edit-repository-flags)
    - [`gh repo fork [<repository>] [-- <gitflags>...] [flags]`](#gh-repo-fork-repository----gitflags-flags)
    - [`gh repo sync [<destination-repository>] [flags]`](#gh-repo-sync-destination-repository-flags)

## `gh auth`

### `gh auth login [flags]`

Authenticate with a GitHub host.

```bash
# start interactive setup
$ gh auth login
# authenticate against github.com by reading the token from a file
$ gh auth login --with-token < mytoken.txt
# authenticate with a specific GitHub instance
$ gh auth login --hostname enterprise.internal
```

- `-p`, `--git-protocol <string>` : Preferred git protocol to use with SSH authentication (defaults to "https", may be "ssh")
- `-h`, `--hostname <string>` : Hostname of GitHub Enterprise instance to authenticate with
- `-w`, `--web` : Open a web browser to authenticate
- `-s`, `--scopes <string>` : Additional authentication scopes for gh to have

### `gh auth logout`

Log out of the CLI by deleting the token on your computer.

```bash
gh auth logout
```

- `-h`, `--hostname <string>` : Hostname of GitHub Enterprise instance to log out of

### `gh auth refresh [flags]`

Expand or fix the permission scopes for stored credentials.

```bash
$ gh auth refresh --scopes write:org,read:public_key
# => open a browser to add write:org and read:public_key scopes for use with gh api
$ gh auth refresh
# => open a browser to ensure your authentication credentials have the correct minimum scopes
```

- `-h` , `--hostname <string>` : Hostname of GitHub Enterprise instance to refresh
- `-s` , `--scopes <string>` : Additional authentication scopes for gh to have

### `gh auth setup-git [flags]`

Configure Git to use credential caching.

```bash
# Configure git to use GitHub CLI as the credential helper for all authenticated hosts
$ gh auth setup-git
# Configure git to use GitHub CLI as the credential helper for enterprise.internal host
$ gh auth setup-git --hostname enterprise.internal
```

`-h`, `--hostname <string>` : The hostname to configure git for

### `gh auth status [flags]`

Show the authentication status.

```bash
gh auth status
```

- `-h`, `--hostname <string>` : Hostname of GitHub Enterprise instance to check status for
- `-t`, `--show-token` : Show only the token on stdout

### `gh auth token [flags]`

Print your OAuth2 token.

```bash
gh auth token
```

- `-h`, `--hostname <string>` : Hostname of GitHub Enterprise instance to check status for

## `gh repo`

### Repository Fields

- assignableUsers
- codeOfConduct
- contactLinks
- createdAt
- defaultBranchRef
- deleteBranchOnMerge
- description
- diskUsage
- forkCount
- fundingLinks
- hasDiscussionsEnabled
- hasIssuesEnabled
- hasProjectsEnabled
- hasWikiEnabled
- homepageUrl
- id
- isArchived
- isBlankIssuesEnabled
- isEmpty
- isFork
- isInOrganization
- isMirror
- isPrivate
- isSecurityPolicyEnabled
- isTemplate
- isUserConfigurationRepository
- issueTemplates
- issues
- labels
- languages
- latestRelease
- licenseInfo
- mentionableUsers
- mergeCommitAllowed
- milestones
- mirrorUrl
- name
- nameWithOwner
- openGraphImageUrl
- owner
- parent
- primaryLanguage
- projects
- pullRequestTemplates
- pullRequests
- pushedAt
- rebaseMergeAllowed
- repositoryTopics
- securityPolicyUrl
- squashMergeAllowed
- sshUrl
- stargazerCount
- templateRepository
- updatedAt
- url
- usesCustomOpenGraphImage
- viewerCanAdminister
- viewerDefaultCommitEmail
- viewerDefaultMergeMethod
- viewerHasStarred
- viewerPermission
- viewerPossibleCommitEmails
- viewerSubscription
- visibility
- watchers

### `gh repo create [<name>] [flags]`

Create a new GitHub repository.

- `--add-readme` : Add a README.md to the new repository
- `-c`, `--clone` : Clone the new repository locally
- `-d`, `--description <string>` : Description of repository
- `-g`, `--gitignore <string>` : Choose a gitignore template (use the special value "list" to see all choices) `Node,Python,Java,TeX,Go,C++,C,Shell,Ruby`
- `-h`, `--homepage <URL>` : Repository home page URL
- `--internal` : Make the new repository internal.
- `--private` : Make the new repository private.
- `--public` : Make the new repository public.
- `--push` : Add remote for origin and push to it.
- `-r`,`--remote <string>` : Specify remote name for the new repository
- `-s`,`--source <string>` : Specify path to local repository to use as source

```bash
# create a repository interactively
gh repo create
# create a new remote repository and clone it locally
gh repo create my-project --public --clone
# create a remote repository from the current directory
gh repo create my-project --private --source=. --remote=upstream
```

```bash
gh repo create working-with-github-cli --public --gitignore Node --clone
```

### `gh repo list [<owner>] [flags]`

List repositories owned by user or organization

- `-L`, `--limit <int>` : Maximum number of repositories to fetch (default 30)
- `--archived` : Show only archived repositories
- `--fork` : Show only forked repositories
- `--json <fields>` : Select fields for JSON output. `<fields>` separated by comma
- `-l` , `--language <string>` : Filter by primary coding language.
- `--source` : Show only non-forks.
- `--topic <string>` : Filter by topic.
- `--visibility <string>` : Filter by repository visibility: {`public`|`private`|`internal`}

```bash
gh repo list -L 1 --json id
gh repo list -L 1 --json id,url
gh repo list pyscript -L 2
gh repo list -l typescript
gh repo list --fork
```

### `gh repo rename <new-name> [flags]`

Rename a GitHub repository.
By default, this renames the current repository; otherwise renames the specified repository.

- `-y`, `--yes` : Skip confirmation prompt
- `-R`, `--repo <string>` : Select another repository using the `HOST/]OWNER/REPO` format

```bash
gh repo rename working-with-github-cli -y
```

### `gh repo view <repository> [flags]`

Display the description and the README of a GitHub repository. With no argument, the repository for the current directory is displayed.

- `b`, `--branch <string>` : The branch to view.
- `--json <fields>` : Select fields for JSON output. `<fields>` separated by comma
- `-w`, `--web` : Open a browser to show the repository

```bash
gh repo view --json name,description
gh repo view -w
```

### `gh repo archive <repository> [flags]`

Archive a GitHub repository.With no argument, archives the current repository.

- `-y`, `--yes` : Skip confirmation prompt

```bash
gh repo archive -y
```

### `gh repo clone  [<directory>] [-- <gitflags>...]`

If the **"OWNER/"** portion of the **"OWNER/REPO"** repository argument is omitted, it defaults to the name of the **authenticating user**.

- `-u`, `--upstream-remote-name <string>>` : Upstream remote name when cloning a fork

```bash
gh repo clone working-with-github-cli
gh repo clone sizar/working-with-github-cli
```

### `gh repo delete`

Delete a GitHub repository. With no argument, deletes the current repository. Otherwise, deletes the specified repository. Deletion requires authorization with the **"delete_repo" scope**. To authorize, run "`gh auth refresh -s delete_repo`"

### `gh repo edit [<repository>] [flags]`

Edit repository settings.

- `--add-topic <strings>` : Add topics
- `--remove-topic <strings>` : Remove topics
- `--allow-forking` : Allow forking
- `--allow-update-branch` : Allow a pull request head branch that is behind its base branch to be updated
- `--default-branch <name>` : Change the default branch
- `--delete-branch-on-merge` : Automatically delete head branches after a pull request is merged\
- `-d`, `--description <string>` : Description of repository
- `--enable-auto-merge` : Enable auto-merge functionality
- `--enable-issues` : Enable issues
- `--enable-merge-commit` : Enable merging pull requests via merge commit
- `--enable-discussions` : Enable discussions
- `--enable-projects` : Enable projects in the repository
- `--enable-rebase-merge` : Enable merging pull requests via rebase
- `--enable-squash-merge` : Enable merging pull requests via squashed commit
- `-h`, `--homepage <URL>` : Repository home page URL
- `--visibility <string>` : Change repository visibility: {`public`|`private`|`internal`}

```bash
gh repo edit --enable-wiki=false
gh repo edit --add-topic cli
gh repo edit --remove-topic cli
gh repo edit --description "A command-line tool for working with GitHub from your terminal."
# enable issues and wiki
gh repo edit --enable-issues --enable-wiki
# disable projects
gh repo edit --enable-projects=false
```

### `gh repo fork [<repository>] [-- <gitflags>...] [flags]`

Create a fork of a repository. With no argument, creates a fork of the current repository. Otherwise, forks the specified repository.By default, the new fork is set to be your "origin" remote and any existing origin remote is renamed to "upstream". To alter this behavior, you can set a name for the new fork's remote with `--remote-name`.

Additional git clone flags can be passed after `--`.

- `--clone` : Clone the fork
- `--default-branch-only` : Only include the default branch in the fork
- `--fork-name <string>` : Rename the forked repository
- `--org <string>` : Create the fork in an organization
- `--remote` : Add a git remote for the fork
- `--remote-name <string>` : Specify the name for the new remote

### `gh repo sync [<destination-repository>] [flags]`

Without an argument, the local repository is selected as the destination repository. The source repository is the parent of the destination repository by default. This can be overridden with the `--source` flag.

- `-b, --branch <string>` : Branch to sync (default: main branch)
- `--force` : Hard reset the branch of the destination repository to match the source repository
- `-s, --source <string>` : Source repository

```bash
# Sync local repository from remote parent
$ gh repo sync
# Sync local repository from remote parent on specific branch
$ gh repo sync --branch v1
# Sync remote fork from its parent
$ gh repo sync owner/cli-fork
# Sync remote repository from another remote repository
$ gh repo sync owner/repo --source owner2/repo2
```
