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
  - [`gh pr`](#gh-pr)
    - [Pull Requests fields](#pull-requests-fields)
    - [`gh pr create [flags]`](#gh-pr-create-flags)
    - [`gh pr edit [<number> | <url> | <branch>] [flags]`](#gh-pr-edit-number--url--branch-flags)
    - [`gh pr list [flags]`](#gh-pr-list-flags)
    - [`gh pr status [flags]`](#gh-pr-status-flags)
    - [`gh pr view [<number> | <url> | <branch>] [flags]`](#gh-pr-view-number--url--branch-flags)
    - [`gh pr checkout [<number> | <url> | <branch>] [flags]`](#gh-pr-checkout-number--url--branch-flags)
    - [`gh pr checks [<number> | <url> | <branch>] [flags]`](#gh-pr-checks-number--url--branch-flags)
    - [`gh pr close [<number> | <url> | <branch>] [flags]`](#gh-pr-close-number--url--branch-flags)
    - [`gh pr comment [<number> | <url> | <branch>] [flags]`](#gh-pr-comment-number--url--branch-flags)
    - [`gh pr diff [<number> | <url> | <branch>] [flags]`](#gh-pr-diff-number--url--branch-flags)
    - [`gh pr merge [<number> | <url> | <branch>] [flags]`](#gh-pr-merge-number--url--branch-flags)
    - [`gh pr ready [<number> | <url> | <branch>] [flags]`](#gh-pr-ready-number--url--branch-flags)
    - [`gh pr reopen [<number> | <url> | <branch>] [flags]`](#gh-pr-reopen-number--url--branch-flags)
    - [`gh pr lock {<number> | <url>} [flags]`](#gh-pr-lock-number--url-flags)
    - [`gh pr unlock {<number> | <url>} [flags]`](#gh-pr-unlock-number--url-flags)
    - [`gh pr review [<number> | <url> | <branch>] [flags]`](#gh-pr-review-number--url--branch-flags)
  - [`gh gist`](#gh-gist)
    - [`gh gist list [flags]`](#gh-gist-list-flags)
    - [`gh gist view [<id> | <url>] [flags]`](#gh-gist-view-id--url-flags)
    - [`gh gist create [<filename>] [flags]`](#gh-gist-create-filename-flags)
    - [`gh gist rename {<id> | <url>} <oldFilename> <newFilename>`](#gh-gist-rename-id--url-oldfilename-newfilename)
    - [`gh gist delete {<id> | <url>}`](#gh-gist-delete-id--url)
    - [`gh gist clone <gist> [<directory>] [-- <gitFlags>...]`](#gh-gist-clone-gist-directory----gitflags)
  - [`gh issue`](#gh-issue)
    - [`gh issue list [flags]`](#gh-issue-list-flags)
    - [`gh issue create [flags]`](#gh-issue-create-flags)
    - [`gh issue status [flags]`](#gh-issue-status-flags)
    - [`gh issue close {<number> | <url>} [flags]`](#gh-issue-close-number--url-flags)
    - [`gh issue comment {<number> | <url>} [flags]`](#gh-issue-comment-number--url-flags)
    - [`gh issue delete {<number> | <url>}`](#gh-issue-delete-number--url)
    - [`gh issue develop {<number> | <url>} [flags]`](#gh-issue-develop-number--url-flags)
    - [`gh issue edit {<number> | <url>} [flags]`](#gh-issue-edit-number--url-flags)
    - [`gh issue lock {<number> | <url>} [flags]`](#gh-issue-lock-number--url-flags)
    - [`gh issue unlock {<number> | <url>} [flags]`](#gh-issue-unlock-number--url-flags)
    - [`gh issue pin  {<number> | <url>} [flags]`](#gh-issue-pin--number--url-flags)
    - [`gh issue reopen {<number> | <url>} [flags]`](#gh-issue-reopen-number--url-flags)

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

## `gh pr`

### Pull Requests fields

- additions
- assignees
- author
- autoMergeRequest
- baseRefName
- body
- changedFiles
- closed
- closedAt
- comments
- commits
- createdAt
- deletions
- files
- headRefName
- headRefOid
- headRepository
- headRepositoryOwner
- id
- isCrossRepository
- isDraft
- labels
- latestReviews
- maintainerCanModify
- mergeCommit
- mergeStateStatus
- mergeable
- mergedAt
- mergedBy
- milestone
- number
- potentialMergeCommit
- projectCards
- projectItems
- reactionGroups
- reviewDecision
- reviewRequests
- reviews
- state
- statusCheckRollup
- title
- updatedAt
- url

### `gh pr create [flags]`

Create a pull request on GitHub.

When the current branch isn't fully pushed to a git remote, a prompt will ask where to push the branch and offer an option to fork the base repository. Use `--head` to explicitly skip any forking or pushing behavior. Adding a pull request to projects requires authorization with the "`project`" scope. To authorize, run "`gh auth refresh -s project`".

- `-a`, `--assignee <login>` : Assign people by their login. Use "@me" to self-assign.
- `-B`, `--base <branch>` : The branch into which you want your code merged
- `-b`, `--body <string>` :Body for the pull request
- `-d`, `--draft` : Mark pull request as a draft
- `-f`, `--fill` : Do not prompt for title/body and just use commit info
- `-H`, `--head <branch>` : The branch that contains commits for your pull request (default: current branch)
- `-l`, `--label <name>` : Add labels by name
- `-p`, `--project <name>` : Add the pull request to projects by name
- `-r`, `--reviewer <handle>` : Request reviews from people or teams by their handle
- `-t`, `--title <string>` : Title for the pull request
- `-w`, `--web` : Open the web browser to create a pull request

```bash
# Create a pull request interactively
# Creating pull request for feature-branch into main in owner/repo
gh pr create
? Title My new pull request
? Body [(e) to launch nano, enter to skip]
gh pr create --title "Pull request title" --body "Pull request body"
```

### `gh pr edit [<number> | <url> | <branch>] [flags]`

Edit a pull request. Without an argument, the pull request that belongs to the current branch is selected.

- `-a`, `--assignee <login>` : Assign people by their login. Use "@me" to self-assign.
- `-B`, `--base <branch>` : The branch into which you want your code merged
- `-b`, `--body <string>` :Body for the pull request
- `-d`, `--draft` : Mark pull request as a draft
- `-f`, `--fill` : Do not prompt for title/body and just use commit info
- `-H`, `--head <branch>` : The branch that contains commits for your pull request (default: current branch)
- `-l`, `--label <name>` : Add labels by name
- `-p`, `--project <name>` : Add the pull request to projects by name
- `-r`, `--reviewer <handle>` : Request reviews from people or teams by their handle
- `-t`, `--title <string>` : Title for the pull request
- `-w`, `--web` : Open the web browser to create a pull request

```bash
gh pr edit 23 --title "I found a bug" --body "Nothing works"
gh pr edit 23 --add-label "bug,help wanted" --remove-label "core"
gh pr edit 23 --add-reviewer monalisa,hubot  --remove-reviewer myorg/team-name
gh pr edit 23 --add-assignee "@me" --remove-assignee monalisa,hubot
gh pr edit 23 --add-project "Roadmap" --remove-project v1,v2
gh pr edit 23 --milestone "Version 1"
```

### `gh pr list [flags]`

List pull requests in a GitHub repository.

- `--app <string>` : Filter by GitHub App author
- `-a`, `--assignee <string>` : Filter by assignee
- `-A`, `--author <string>` : Filter by author
- `-B`, `--base <string>` : Filter by base branch
- `-d`, `--draft` : Filter by draft state
- `-H`, `--head <string>` : Filter by head branch
- `-q`, `--jq <expression>` : Filter JSON output using a jq expression
- `--json <fields>` : Output JSON with the specified fields
- `-l`, `--label <strings>` : Filter by label
- `-L`, `--limit <int>` : Maximum number of items to fetch
- `-S`, `--search <query>` : Search pull requests with query
- `-s`, `--state <string>` : Filter by state: {open|closed|merged|all}
- `-t`, `--template <string>` : Format JSON output using a Go template; see "gh help formatting"
- `-w`, `--web` : List pull requests in the web browser

```bash
# List PRs authored by you
$ gh pr list --author "@me"
# List only PRs with all of the given labels
$ gh pr list --label bug --label "priority 1"
# Filter PRs using search syntax
$ gh pr list --search "status:success review:required"
# Find a PR that introduced a given commit
$ gh pr list --search "<SHA>" --state merged
```

### `gh pr status [flags]`

- `-c`, `--conflict-status` : Display the merge conflict status of each pull request
- `-q`, `--jq <expression>` : Filter JSON output using a jq expression
- `--json <fields>` : Output JSON with the specified fields

### `gh pr view [<number> | <url> | <branch>] [flags]`

Display the title, body, and other information about a pull request.

- `-c, --comments` : View pull request comments
- `--json <fields>` :Output JSON with the specified field
- `-w, --web` : Open a pull request in the browser

```bash
# Viewing a pull request in terminal
gh pr view 21
# Viewing a pull request in the browser
gh pr view 21 --web
```

### `gh pr checkout [<number> | <url> | <branch>] [flags]`

Check out a pull request in git.

- `-b, --create-branch` : Create a new branch for this pull request. Local branch name to use (default: the name of the head branch)
- `--detach` : Checkout PR with a detached HEAD
- `-f`, `--force` : Reset the existing local branch to the latest state of the pull request
- `--recurse-submodules` : Update all submodules after checkout

```bash
# Checking out a pull request locally
gh pr checkout 12
gh pr checkout branch-name
```

### `gh pr checks [<number> | <url> | <branch>] [flags]`

Show CI status for a single pull request.

### `gh pr close [<number> | <url> | <branch>] [flags]`

- `-c`, `--comment <string>` : Leave a closing comment
- `-d`, `--delete-branch` : Delete the local and remote branch after close

### `gh pr comment [<number> | <url> | <branch>] [flags]`

- `-b`, `--body <text>` : The comment body text
- `--edit-last` : Edit the last comment of the same author
- `-e`, `--editor` : Skip prompts and open the text editor to write the body in
- `-w`, `--web` : Open the web browser to write the comment

### `gh pr diff [<number> | <url> | <branch>] [flags]`

View changes in a pull request.
Without an argument, the pull request that belongs to the current branch is selected.

- `--color <string>` : Use color in diff output: {always|never|auto}
- `--name-only` : Display only names of changed files
- `--patch` : Display diff in patch format
- `-w`, `--web` : Open the pull request diff in the browser

### `gh pr merge [<number> | <url> | <branch>] [flags]`

Merge a pull request on GitHub.
Without an argument, the pull request that belongs to the current branch is selected.

- `--admin` : Use administrator privileges to merge a pull request that does not meet requirements
- `-A`, `--author-email <text>` : Email text for merge commit author
- `--auto` : Automatically merge only after necessary requirements are met
- `-b`, `--body <text>` : Body text for the merge commit
- `-F`, `--body-file <file>` : Read body text from file (use "-" to read from standard input)
- `-d`, `--delete-branch` : Delete the local and remote branch after merge
- `--disable-auto` : Disable auto-merge for this pull request
- `--match-head-commit <SHA>` : Commit SHA that the pull request head must match to allow merge
- `-m`, `--merge` : Merge the commits with the base branch
- `-r`, `--rebase` : Rebase the commits onto the base branch
- `-s`, `--squash` : Squash the commits into one commit and merge it into the base branch
- `-t`, `--subject <text>` : Subject text for the merge commit

### `gh pr ready [<number> | <url> | <branch>] [flags]`

Mark a pull request as ready for review.

### `gh pr reopen [<number> | <url> | <branch>] [flags]`

- `-c`, `--comment <string>` Leave a comment when reopening

### `gh pr lock {<number> | <url>} [flags]`

Lock pull request conversation

`-r`, `--reason <string>` : Optional reason for locking conversation (off_topic, resolved, spam, too_heated).

### `gh pr unlock {<number> | <url>} [flags]`

Unlock pull request conversation

### `gh pr review [<number> | <url> | <branch>] [flags]`

Add a review to a pull request. Without an argument, the pull request that belongs to the current branch is reviewed.

- `-a`, `--approve` : Approve pull request
- `-b`, `--body <string>` : Specify the body of a review
- `-F`, `--body-file <file>` : Read body text from file (use "-" to read from standard input)
- `-c`, `--comment` : Comment on a pull request
- `-r`, `--request-changes` : Request changes on a pull request

```bash
# approve the pull request of the current branch
$ gh pr review --approve
# leave a review comment for the current branch
$ gh pr review --comment -b "interesting"
# add a review for a specific pull request
$ gh pr review 123
# request changes on a specific pull request
$ gh pr review 123 -r -b "needs more ASCII art"
```

## `gh gist`

### `gh gist list [flags]`

- `-L`, `--limit <int>` : Maximum number of gists to fetch
- `--public` : Show only public gists
- `--secret` : Show only secret gists

```bash
# List all gists
$ gh gist list
# List only public gists
$ gh gist list --public
# List only secret gists
$ gh gist list --secret
```

### `gh gist view [<id> | <url>] [flags]`

- `-w`, `--web` : Open gist in the browser
- `-f`, `--filename <string>` : Select a file to view
- `-r`, `--raw` : View the raw contents of a gist file
- `--files` : List gist files with line counts and language identifiers

```bash
# View a gist in the browser
$ gh gist view 123 --web
# View a specific file in a gist
$ gh gist view 123 --filename hello.py
# View the raw contents of a gist file
$ gh gist view 123 --filename hello.py --raw
```

### `gh gist create [<filename>] [flags]`

- `-d`, `--desc <string>` : Description of the gist
- `-p`, `--public` : List the gist publicly (default: secret)
- `-f`, `--filename <string>` : Provide a filename to be used when reading from STDIN

```bash
# publish file 'hello.py' as a public gist
$ gh gist create --public hello.py
# create a gist with a description
$ gh gist create hello.py -d "my Hello-World program in Python"
# create a gist containing several files
$ gh gist create hello.py world.py cool.txt
# read from standard input to create a gist
$ gh gist create -
# create a gist from output piped from another command
$ cat cool.txt | gh gist create
```

`gh gist edit {<id> | <url>} [<filename>] [flags]`

- `-d`, `--desc <string>` : Description of the gist
- `-f`, `--filename <string>` : Select a file to edit
- `-a`, `--add <string>` : Add a new file to the gist

```bash
# edit a gist
$ gh gist edit 123456
# edit a specific file in a gist
$ gh gist edit 123456 hello.py
```

### `gh gist rename {<id> | <url>} <oldFilename> <newFilename>`

```bash
gh gist rename b755ac492a9498b2fc8ed1772098
b0ef gistfile0.txt hi.txt
```

### `gh gist delete {<id> | <url>}`

```bash
gh gist delete <id>
```

### `gh gist clone <gist> [<directory>] [-- <gitFlags>...]`

Clone a GitHub gist locally.

## `gh issue`

### `gh issue list [flags]`

List and filter issues in this repository.

- `-a`, `--assignee <string>` : Filter by assignee.
- `-A`, `--author <string>` : Filter by author.
- `-L`, `--limit <int>` : Maximum number of issues to fetch (default 30).
- `-l`, `--label <string>` : Filter by label.
- `--mention <string>` : Filter by mention.
- `-m`, `--milestone <string>` : Filter by milestone.
- `-s` , `--state <string>` : Filter by state: {`open`|`closed`|`all`} (default "open").
- `-w`, `--web` : Open the browser to list the issue on GitHub.
- `-t`, `--template <string>` : Format JSON output using a Go template".

```bash
# List all issues
gh issue list
# List all issues assigned to you
gh issue list --assignee '@me'
# List all issues with the "bug" label
gh issue list --label 'bug'
# List all issues in the "v1" milestone
gh issue list --milestone 'v1'
#List all issues including those closed.
gh issue list --state all
```

### `gh issue create [flags]`

Create a new issue.

- `-a`, `--assignee <string>` : Assign people by their login. Use "@me" to self-assign.
- `-b`, `--body <string>` : Body for the issue.
- `l`, `--label <strings>` : Add labels by name.
- `-m`, `--milestone <string>` : Add the issue to a milestone by name.
- `-p`, `--project <string>` : Add the issue to projects by name.
- `-t`, `--title <string>` : Title for the issue.
- `-T`, `--template <string>` : Template for the issue's body.
- `-w`, `--web` : Open the browser to create an issue.
- `-recover` : Recover input from a failed run of `gh issue create`.

```bash
# Basic usage with a title
gh issue create --title "A new issue"
# With a title and body
gh issue create --title "A new issue" --body "This is the body of the issue"
# Assigning the issue to a user
gh issue create --title "A new issue" --assignee "username"
# Assigning the issue to yourself
gh issue create --title "A new issue" --assignee "@me"
# Adding labels to the issue
gh issue create --title "A new issue" --label "bug,ui"
# Adding the issue to a milestone
gh issue create --title "A new issue" --milestone "Milestone1"
# Adding the issue to a project
gh issue create --title "A new issue" --project "Project1"
# Using a template for the issue's body
gh issue create --title "A new issue" --template "template.md"
# Opening the browser to create an issue
gh issue create --web
# Recovering input from a failed run
gh issue create --recover
```

### `gh issue status [flags]`

Show status of relevant issues.

- `-q`, `--jq <expression>` : Filter JSON output using a jq expression.
- `--json <fields>` : Output JSON with the specified fields.

```bash
# Show status of relevant issues
gh issue status
# Show status of relevant issues in JSON format
gh issue status --json number,title,url
```

### `gh issue close {<number> | <url>} [flags]`

Close an issue.

- `-c`, `--comment <string>` : Add a comment to the issue.
- `-r`, `-reason <string>` : Reason for closing the issue: {`completed`|`not planned`}

```bash
# Close an issue
gh issue close 123
# Close an issue with a comment
gh issue close 123 -c "I fixed this"
```

### `gh issue comment {<number> | <url>} [flags]`

Add a comment to an issue.

- `-b`, `--body <string>` : Body of the comment.
- `-e`, `--editor` : Add body using editor.
- `-w`, `--web` : Add comment in browser.

```bash
# Add a comment to an issue
gh issue comment 123 -b "I think this is a bug"
# Add a comment to an issue using an editor
gh issue comment 123 -e
# Add a comment to an issue in the browser
gh issue comment 123 -w
```

### `gh issue delete {<number> | <url>}`

Delete an issue.

```bash
# Delete an issue
gh issue delete 123
# Delete without confirmation prompt
gh issue delete 123 --yes
```

### `gh issue develop {<number> | <url>} [flags]`

Manage linked branches for an issue

- `-b`, `--base <string>` : Name of the base branch you want to make your new branch from.
- `--branch-repo <string>` : Name or URL of the repository where you want to create your new branch
- `-c`, `--checkout` : Check out the new branch after creating it.
- `-l`, `--list` : List linked branches for this issue.
- `-n`,`--name <string>` : Name of the new branch.

```bash
# List branches for issue 123
gh issue develop --list 123
# List branches for issue 123 in repo cli/cli
gh issue develop --list --repo cli/cli 123
# Create a branch for issue 123 based on the my-feature branch
gh issue develop 123 --base my-feature
# Create a branch for issue 123 and checkout it out
gh issue develop 123 --checkout
# Create a branch in repo unknown/cli for issue 123 in repo cli/cli
gh issue develop 123 --repo cli/cli --branch-repo unknown/cli
```

### `gh issue edit {<number> | <url>} [flags]`

Edit an issue.

- `--add-assignee <string>` : Add assignee by their login. Use "@me" to self-assign.
- `--add-label <strings>` : Add labels by name.
- `--add-project <string>` : Add the issue to projects by name.
- `-b`, `--body <string>` : Body for the issue.
- `--remove-assignee <string>` : Remove assignee by their login.
- `--remove-label <strings>` : Remove labels by name.
- `--remove-project <string>` : Remove the issue from projects by name.
- `-t`, `--title <string>` : Title for the issue.
- `-m`, `--milestone <string>` : Edit the milestone the issue belongs to by name.

```bash
# Edit an issue
gh issue edit 123 --title "A better title" --body "A better description"
# Edit an issue's assignee
gh issue edit 123 --add-assignee "username"
# Edit an issue's labels
gh issue edit 123 --add-label "bug,ui"
# Edit an issue's milestone
gh issue edit 123 --milestone "Milestone1"
# Edit an issue's project
gh issue edit 123 --add-project "Project1"
# Edit an issue's assignee, labels, and milestone
gh issue edit 123 --add-assignee "username" --add-label "bug,ui" --milestone "Milestone1"
```

### `gh issue lock {<number> | <url>} [flags]`

Lock an issue's conversation.

- `-r`, `--reason <string>` : Reason for locking the issue: {`off-topic`|`resolved`|`spam`|`too_heated`}

```bash
# Lock an issue's conversation
gh issue lock 123
# Lock an issue's conversation with a reason
gh issue lock 123 --reason "resolved"
```

### `gh issue unlock {<number> | <url>} [flags]`

Unlock an issue's conversation.

```bash
# Unlock an issue's conversation
gh issue unlock 123
```

### `gh issue pin  {<number> | <url>} [flags]`

Pin an issue to the top of the issue list.

```bash
# Pin an issue to the top of the issue list

gh issue pin 123
```

### `gh issue reopen {<number> | <url>} [flags]`

Reopen a closed issue.

- `-c` , `--comment <string>` : Add a comment to the issue.

```bash
# Reopen a closed issue
gh issue reopen 123
# Reopen a closed issue with a comment
gh issue reopen 123 --comment "I think this is a bug"
```
