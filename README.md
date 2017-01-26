## Welcome

First of all, thank you for your interest in helping maintain software in this
organization's repos. Your help is greatly appreciated!

## Slack

All maintainers should join the House Absolute Slack for discussion of our
projects. If you haven't received an invite, contact Dave Rolsky
(autarch@urth.org or autarch on irc.perl.org) and tell him what email address
he should use to invite you.

## Access Rights

As a maintainer, you should have administrator access to any relevant
repos. This will let you set up things like Travis and AppVeyor integrations,
Slack notifications, etc. You can also add new maintainers and generally do
whatever you want.

However, before you do anything, please ask in the relevant Slack
channel. Since we have a number of people involved in these projects, it's
good to give folks a heads up before making changes to A) make sure everyone's
on board; and B) make sure no one else is working on the same thing.

## Making Changes to the Code

Unless you are Dave Rolsky, please do not commit directly to master. The only
exceptions are straightforward typo fixes (missing words, misspellings, etc.).

All other changes should be pushed in a branch to the main repo and submitted
as a GitHub pull request.

### Branch Contents

Each branch should be as small as possible. If you want to add two unrelated
features, make two branches. If you want to add two very closely related
features, or fix two closely related bugs, you can put them in a single
branch, but it wouldn't hurt to provide two branches, with one building on top
of the other.

### Commit Contents

Break your commits up into self-contained units. All of the changes for a
single logical step should be added together. So for example, if you are
fixing a bug, then the tests, bug fix, and `Changes` entry for that fix should
all come in a single commit. Do not make three commits, one for the test, one
for the fix, and one for the Changes entry.

If you want to make unrelated refactoring, code tidying, or other cleanup
changes, please put those in separate commits whenever possible. It's okay to
put them in the same branch as a bug fix or feature, however.

### Tidyall

All distros should include both `perlcriticrc` and `perltidyrc` files. You can
use [`tidyall`](https://metacpan.org/release/Code-TidyAll) to tidy all your
code and run the critic checks before submitting a branch. You can tidy all
the code in a repo with `tidyall -a` and tidy just the those things which have
been changed with `tidyall -g`.

To install `tidyall` run `cpanm Code::TidyAll`.

### Commit Messages

From [Chris Beams](http://chris.beams.io/posts/git-commit/) ...

1. Separate subject from body with a blank line
2. Limit the subject line to 75 characters (Chris says 50, but a little longer is ok)
3. Capitalize the subject line
4. Do not end the subject line with a period
5. Use the imperative mood in the subject line
6. Wrap the body at 78 characters (Chris says 72, Dave says 78, just use something less than 80)
7. Use the body to explain what and why vs. how

All of these are pretty obvious, except for #5, which means that you should
write these in present tense, starting with a verb, and with no pronoun. So
something like "Add tests for time zone boundaries". Do not write "Added tests
..." (past tense) or "I added tests ..." (pronoun), etc.

Please read the whole post from Chris for more details.

## Reviewing PRs

All pull requests must be reviewed by one or more maintainers. Use
GitHub's
[pull request review](https://help.github.com/articles/about-pull-request-reviews/) feature
to do your reviews. In general, you should submit the review with either the
"Approve" or "Request changes" status so the contributor knows what the next steps are.

A PR cannot be merged until it passes in Travis (and AppVeyor, if relevant).

## Responding to Review Comments

Please rebase your PR in response to comments. This lets us avoid having lots
of commits like "fixing spelling in a comment" or "renaming $foo variable".

## Merging PRs

For now, Dave Rolsky will be the only one to merge PRs. However, he will not
merge anything (including his own changes) without having them reviewed and
approved by one other contributor. The only exception will be PRs for trivial
changes such as typo fixes, small documentation updates, etc. Code changes
should always be reviewed by at least one other maintainer.

## PAUSE Releases

Dave Rolsky will be the only one to do these for now.

## Dist::Zilla

All of the houseabsolute distributions should use `Dist::Zilla` and
the [`DROLSKY`](https://metacpan.org/release/Dist-Zilla-PluginBundle-DROLSKY)
plugin bundle. This bundle does a lot of stuff, including:

* Automatically adding module prereqs for all phases.
* Munging documentation to add various bits of boilerplate.
* Generating things like `README.md` and `CONTRIBUTING.md` files.
* Adding many release/author tests such as pod spelling, Changes formatting, etc.
* Testing that all files pass tidy and `Perl::Critic` checks.
* Adding contributor info to the POD and distro meta-info.
* Uploading the release tarball to PAUSE.
* Tagging the release in the git repo.
* Copying all generated files like `Makefile.PL` into the repo and committing
  them so that casual contributors don't have to use dzil.
* Bumping the `$VERSION` in all files and commiting this change.
* Pushing those post-release commits.

You can make sure that your changes pass *all* tests by running `dzil test
--release` in the repo root. To run tests in parallel add something like `-j
6`.
