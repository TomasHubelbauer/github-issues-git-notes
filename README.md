# GitHub Issues Git Notes GitHub Action

[Git Notes]: https://git-scm.com/docs/git-notes
[`issues`]: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#issues

This GitHub Action stores the API payload from the `GET /issues` API call into
the Git notes ref of the repository it has run for.

This repository implements a GitHub Actions that takes the GitHub Issues (backed
by the GitHub database not the Git objects) of the  GitHub repository it runs on
using the GitHub API and stores the JSON in the Git repository's [Git Notes].

This action should be run on all [`issues`] related trigger events. See the
[demo](https://github.com/TomasHubelbauer/github-issues-git-notes-demo).

Git notes are pushed back to the repository using `git push origin refs/notes/*`
and with the GitHub Actions Git identity.

The note is added to the repository's default branch's ref, associated to the
branch's tip commit. If the workflow runs multiple times for the same commit, it
will update the note for that commit.

Git notes can be fetched locally by using `git fetch` with the `notes` ref:
`git fetch origin "refs/notes/*:refs/notes/*"`. Avoid managing Git notes locally
as you'll be responsible for merging the local and remote changes in that case.

To view notes for the `main` branch, run the Git `log` command with `%N` format:
`git log --pretty=format:"%ai%n  %H%n  %s%n  %N%n" --show-notes main`.
