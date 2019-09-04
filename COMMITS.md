# Commit contents and messages

This document builds on [Conventional Commits v1.0](https://www.conventionalcommits.org/en/v1.0.0-beta.4/), filling in guidance where the general standard avoids providing firm positions.

## On rebasing

Features branches should be rebased / squashed as needed before they are merged such that their commit log most accurately reflects these practices. When reviews catch mistakes/oversights in segmenting commits, the author should use rebase to produce a corrected set of commits rather than appending more commits.

Published branches, e.g. `develop` or `releases/*` should never have their history rewritten

## On merging

Feature branches should always be appended to `develop` through a merge commit, do not just fast-forward develop through a set of commits. Merge commits are important in documenting who/when a thread of work got combined into the main development branch. Use them to reference any relevant pull request / issue numbers that caused the set of work.

## Clarified guidance on use of commit prefixes

Consistent use of commit prefixes--and the segmentation of code changes that they force--are a powerful force for making our review and release processes more efficient and reliable.

- `feat`: An addition or tangible change to application behavior
- `fix`: A restoration/support of expected application behavior
- `refactor`: A relocation or reorganization of code that should make no change to application behavior
    - Include both sides of a transformation together in the same commit
    - To the greatest extent practical, seperate `fix`/`feat` changes out into follow-up commits. Go one or two, but not much more, small steps out of your way to make your refactor commit as neutral to application behavior as possible, including moving bugs around if they're isolated well enough within the code being moved. Any fixes you can seperate from the refactor they precipitated will stand out and be best understood within their own commits.
- `chore`: Any codebase housekeeping that *should* have no effect on application behavior

## What we want to get out of this practice

### Help Reviewers do their job well

By giving them the option to break changes into chunks that should be making only one sort of change to the application's behavior or the code's form.

This does not help much in spotting business logic errors, which other validation processes are better at catching, but it enables Reviewers to effectively look for mistakes in the use of code without having to download full context on what the business logic should be.

### Help Releasers do their job well

Looking through a list of commits following these conventions faithfully (which the reviewer should have enforced) helps Releasers know what they need to do just by reading the prefixes contained in a set of commits being released:

- a release containing only `chore` and `refactor` commits can be released with a patch version number and shipped out to users quickly/widely without drawing much of their attention
- a release containing only `fix` commits (or any `fix` commits among only `chore`/`refactor` commits) should be released as above, but passively announced in a way that's easy for users who are actively following development to catch
- a release containing *any* `feat` commits sholud be released with a minor version number and actively announced to users or their proxies
