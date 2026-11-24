GitHub CLI (gh) – Practical Learning Notes

Repository: dikshavarmafr/gitprac
Environment: Ubuntu Docker container
GitHub Username: dikshavarmafr

Task 3: GitHub Issues

1. What is a GitHub Issue?

A GitHub Issue is used to track work that needs to be done in a repository.

It can represent:

A bug or production issue.

A new feature request.

A documentation task.

An improvement or technical debt.

A question or discussion.

Example: A production application is failing because the Docker image cannot be pulled. We can create an issue to track investigation and resolution.

Issue vs Pull Request

Issue

Pull Request

Tracks what needs to be done

Proposes code changes

Used for bugs, tasks and features

Used to merge code

Can be assigned to someone

Can request code reviewers

Can be labelled and discussed

Can be approved or rejected

Remember:

Issue = What needs to be done?

PR = What code changes are proposed to solve it?

2. Create an issue

gh issue create --repo dikshavarmafr/gitprac \
  --title "Improve README documentation" \
  --body "The README needs better documentation." \
  --label "documentation"

If the label doesn't exist, create it first.

3. List open issues

gh issue list --repo dikshavarmafr/gitprac

gh issue list --repo dikshavarmafr/gitprac --state open

4. View a specific issue

gh issue view 2 --repo dikshavarmafr/gitprac

5. Close and reopen an issue

Close:

gh issue close 2 --repo dikshavarmafr/gitprac

Reopen:

gh issue reopen 2 --repo dikshavarmafr/gitprac

6. GitHub labels and colours

Labels categorise issues.

Create a red bug label:

gh label create bug \
  --repo dikshavarmafr/gitprac \
  --color d73a4a

Create a blue documentation label:

gh label create documentation \
  --repo dikshavarmafr/gitprac \
  --color 0075ca

If a label already exists, edit its colour:

gh label edit bug --repo dikshavarmafr/gitprac --color d73a4a

List labels:

gh label list --repo dikshavarmafr/gitprac

Important: Hexadecimal colour codes are provided without #.

Common colours:

Colour

Hex code

Red

d73a4a

Blue

0075ca

Green

0e8a16

Yellow

fbca04

Purple

6f42c1

7. Assign ownership of an issue

Ownership means assigning responsibility to someone who will investigate and resolve the issue.

Assign to yourself:

gh issue edit 2 --repo dikshavarmafr/gitprac --add-assignee @me

Assign to another GitHub user:

gh issue edit 2 --repo dikshavarmafr/gitprac --add-assignee USERNAME

Remove an assignee:

gh issue edit 2 --repo dikshavarmafr/gitprac --remove-assignee USERNAME

Check ownership:

gh issue view 2 --repo dikshavarmafr/gitprac

8. Edit an issue

The gh issue edit command allows us to update an existing issue.

What to edit

Option

Title

--title

Description

--body

Add assignee

--add-assignee

Remove assignee

--remove-assignee

Add label

--add-label

Remove label

--remove-label

Set milestone

--milestone

Remove milestone

--remove-milestone

Examples:

gh issue edit 2 --title "Fix Docker image pull failure"

gh issue edit 2 --body "Investigate the image pull failure."

gh issue edit 2 --add-label bug

gh issue edit 2 --remove-label bug

Add a comment:

gh issue comment 2 --body "Investigation is in progress."

9. Track issue activity

View issue conversation:

gh issue view 2 --repo dikshavarmafr/gitprac --comments

View detailed events using GitHub API:

gh api repos/dikshavarmafr/gitprac/issues/2/events

Display event, username and timestamp:

gh api repos/dikshavarmafr/gitprac/issues/2/events \
  --jq '.[] | [.event, .actor.login, .created_at] | @tsv'

Activity can include:

Issue assignment.

Label changes.

Issue closure or reopening.

Milestone changes.

Why is activity tracking useful?

It provides traceability and accountability. We can identify who performed an action and when.

Task 4: Pull Requests

1. What is a Pull Request?

A Pull Request (PR) is a request to merge changes from one branch into another.

Example:

feature-branch → main

In a real DevOps workflow, developers generally create PRs so that code can be reviewed and tested before merging into the main branch.

2. Create a branch and make changes

Create a new branch:

git switch -c feature-branch

Create a file:

echo "Learning GitHub Pull Requests." > notes.md

Stage and commit:

git add notes.md
git commit -m "Add pull request notes"

Push:

git push -u origin feature-branch

-u establishes upstream tracking, so subsequent pushes can use git push.

3. Create a PR using GitHub CLI

gh pr create \
  --base main \
  --head feature-branch \
  --title "Add pull request notes" \
  --body "This PR adds pull request practice notes."

Meaning:

--base: Target branch.

--head: Source branch.

--title: PR title.

--body: PR description.

4. List open PRs

gh pr list --repo dikshavarmafr/gitprac

List merged PRs:

gh pr list --repo dikshavarmafr/gitprac --state merged

List all PRs:

gh pr list --repo dikshavarmafr/gitprac --state all

5. View PR details

gh pr view 3 --repo dikshavarmafr/gitprac

Get structured information:

gh pr view 3 --repo dikshavarmafr/gitprac \
  --json state,reviewDecision,reviewRequests,statusCheckRollup

Important fields:

Field

Meaning

state

Open, closed or merged

reviewDecision

Review decision

reviewRequests

Requested reviewers

statusCheckRollup

Automated check results

An empty reviewRequests array means no reviewers have been requested.

An empty statusCheckRollup means no status checks are reported.

6. Request a reviewer

gh pr edit 3 --repo dikshavarmafr/gitprac \
  --add-reviewer USERNAME

A reviewer examines the code before it is merged.

7. Inspect PR changes

gh pr diff 3 --repo dikshavarmafr/gitprac

This displays the actual code differences proposed by the PR.

8. Checkout someone else's PR

gh pr checkout 4 --repo dikshavarmafr/gitprac

This downloads and checks out the PR branch locally.

We can then inspect and test the code.

9. Review a PR

There are three main review actions.

Approve:

gh pr review 4 --approve --body "Looks good. Approved."

Comment:

gh pr review 4 --comment --body "Please add error handling."

Request changes:

gh pr review 4 --request-changes --body "Please fix the validation issue."

Note: You generally cannot approve your own PR.

10. Merge a PR

Merge commit:

gh pr merge 3 --repo dikshavarmafr/gitprac --merge

Squash merge:

gh pr merge 3 --repo dikshavarmafr/gitprac --squash

Rebase merge:

gh pr merge 3 --repo dikshavarmafr/gitprac --rebase

Difference between merge methods

Method

Behaviour

Merge

Creates a merge commit and preserves branch history

Squash

Combines PR commits into one commit

Rebase

Replays commits onto the target branch

11. Verify merged changes

gh pr view 3 --repo dikshavarmafr/gitprac

Switch to main:

git switch main

Pull the latest changes:

git pull origin main

Verify the file:

ls
cat pull-requests.md

Important Git concepts: SHA, branch and PR

SHA: Secure Hash Algorithm. Git uses a hash to uniquely identify a commit.

Example:

972985d Add pull request practice notes

Here, 972985d is the shortened commit SHA.

Branch: A movable pointer to a commit representing a line of development.

Pull Request: A request to merge changes from one branch into another.

A PR requires:

A valid source branch.

A valid target branch.

At least one new commit in the source branch that is not already included in the target branch.

Our failed PR attempt happened because pullreq did not exist at that time, and the existing gh-pr changes had already been merged into main.

Task 5: GitHub Actions and Workflows (Preview)

1. What is GitHub Actions?

GitHub Actions is a CI/CD automation platform built into GitHub.

It allows us to automate:

Building applications.

Running unit tests.

Performing security scans.

Deploying applications.

Running scheduled maintenance tasks.

Workflow vs Workflow Run

Workflow: An automated process defined in a YAML file.

Workflow run: One execution of that workflow.

Example: A workflow named Unit Tests can execute every time a developer pushes code. Each execution receives a different run ID.

2. List workflows

gh workflow list --repo cli/cli

This lists configured workflows.

Examples from our practice:

Acceptance Tests.

Unit and Integration Tests.

Deployment.

Code Scanning.

Lint.

3. List workflow runs

gh run list --repo cli/cli --limit 10

This displays recent workflow executions.

4. View a specific workflow run

gh run view RUN_ID --repo cli/cli

Replace RUN_ID with an actual run ID from gh run list.

5. Filter runs by workflow

gh run list --repo cli/cli \
  --workflow 354871894 --limit 5

6. View execution logs

gh run view RUN_ID --repo cli/cli --log

Logs help us investigate build or deployment failures.

7. Other useful workflow commands

gh run watch RUN_ID --repo OWNER/REPO

Monitor a running workflow.

gh run rerun RUN_ID --repo OWNER/REPO

Rerun a workflow.

gh run cancel RUN_ID --repo OWNER/REPO

Cancel a running workflow.

gh workflow view WORKFLOW_NAME --repo OWNER/REPO

View workflow details.

gh workflow run WORKFLOW_NAME --repo OWNER/REPO

Manually trigger a workflow, if it supports the required trigger.

Important difference: Workflow ID vs Run ID

ID

Meaning

Workflow ID

Identifies the configured workflow

Run ID

Identifies one execution of that workflow

We initially used a workflow ID with gh run view, which returned HTTP 404. The correct approach is to obtain a run ID using gh run list.

8. How are these useful in DevOps?

Imagine a developer pushes code.

GitHub Actions triggers a workflow.

The pipeline checks out the code.

It builds the application.

It executes tests.

It performs security scanning.

If successful, deployment can proceed.

If failed, the DevOps engineer investigates the logs.

Interview answer:

"GitHub CLI helps us monitor and manage CI/CD workflows from the terminal. We can check pipeline status, investigate failures through logs, rerun failed workflows and manually trigger workflows. This helps with faster troubleshooting and automation."

Task 6: Useful GitHub CLI Tricks

1. gh api – Direct GitHub API access

gh api allows us to communicate directly with GitHub's REST or GraphQL API.

It is useful when the normal gh commands do not expose all the information or functionality we need.

Get authenticated user information:

gh api user

Get only the username:

gh api user --jq .login

Get repository information:

gh api repos/dikshavarmafr/gitprac

Get repository name:

gh api repos/dikshavarmafr/gitprac --jq .name

List repository branches:

gh api repos/dikshavarmafr/gitprac/branches \
  --jq '.[].name'

List issues:

gh api repos/dikshavarmafr/gitprac/issues

Display issue number, title and state:

gh api repos/dikshavarmafr/gitprac/issues \
  --jq '.[] | [.number, .title, .state] | @tsv'

What is --jq?

--jq filters JSON output using the jq expression language.

Examples:

gh api user --jq .login

Displays only the login/username field.

gh api user --jq .name

Displays the user's name, if available.

2. gh gist – Share code snippets

A GitHub Gist is a way to share small code snippets, configuration files and scripts.

Useful commands:

gh gist list

List your Gists.

gh gist create script.sh

Create a Gist from a file.

gh gist view GIST_ID

View a Gist.

gh gist edit GIST_ID

Edit a Gist.

A private Gist is unlisted, not a secure storage location. Never put passwords, tokens or other secrets in a Gist.

3. gh release – Manage software releases

A release represents a published version of a project.

Example versions:

v1.0.0

v1.1.0

v2.0.0

List releases:

gh release list --repo OWNER/REPO

View a release:

gh release view TAG --repo OWNER/REPO

Create a release:

gh release create v1.0.0 \
  --repo OWNER/REPO \
  --title "Version 1.0.0" \
  --notes "Initial stable release."

Releases are useful for publishing application versions and attaching build artifacts.

4. gh alias – Create shortcuts

Aliases allow us to create shorter commands for frequently used operations.

Create an alias:

gh alias set prs 'pr list --state open'

Now use:

gh prs

Instead of repeatedly typing:

gh pr list --state open

List aliases:

gh alias list

Delete an alias:

gh alias delete prs

5. gh search repos – Search repositories

Search for public repositories directly from the terminal.

Example:

gh search repos docker --limit 10

Search for Terraform repositories:

gh search repos terraform --limit 10

Search by language:

gh search repos kubernetes --language go --limit 10

This is useful when discovering open-source tools, projects and learning resources.

Quick Revision: Commands Learned

Requirement

Command

Create issue

gh issue create

List issues

gh issue list

View issue

gh issue view

Edit issue

gh issue edit

Close issue

gh issue close

Reopen issue

gh issue reopen

Track issue events

gh api .../issues/NUMBER/events

Create PR

gh pr create

List PRs

gh pr list

View PR

gh pr view

View PR diff

gh pr diff

Checkout PR

gh pr checkout

Review PR

gh pr review

Merge PR

gh pr merge

List workflows

gh workflow list

List workflow runs

gh run list

View workflow run

gh run view

View run logs

gh run view --log

GitHub API

gh api

Gists

gh gist

Releases

gh release

Aliases

gh alias

Search repositories

gh search repos

Important DevOps Interview Questions

1. What is a GitHub Issue?

A GitHub Issue is used to track bugs, tasks, feature requests and other work within a repository.

2. What is a Pull Request?

A Pull Request is a request to merge code changes from one branch into another. It allows code review and automated checks before merging.

3. What is the difference between a merge commit and squash merge?

A merge commit preserves individual commits and adds a merge commit, whereas squash combines all PR commits into one commit.

4. How do you investigate a failed GitHub Actions pipeline?

I use gh run list to identify the failed run, gh run view to inspect its details and gh run view --log to investigate the failure.

5. How do you review another developer's PR?

I use gh pr view to inspect details, gh pr diff to review changes, gh pr checkout to test locally and gh pr review to submit feedback.

6. How can GitHub CLI help with DevOps automation?

It can automate issue creation, PR management, workflow monitoring, release management and GitHub API interactions through shell scripts and CI/CD pipelines.

End of today's GitHub CLI learning notes.


