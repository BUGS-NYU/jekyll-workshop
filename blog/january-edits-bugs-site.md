---
title: January 2019 Edits for Bugs Website
date: 2019-01-15
layout: post
permalink: /blog/2019/01/january-edits-bugs-site
---
This is a summary of the edits that I merged into the BUGS website for the month of
January. All of the edits were first merged into the `dev` branch, then committed.
PR can be found at https://github.com/BUGS-NYU/bugs-nyu.github.io/pull/96 and detailed
`diff` report can be found [in this log.][diff-log]

[diff-log]: https://a1liu.github.io/assets/blog/2019/01/january-2019-edits-for-bugs-website/diff.html

### Non-Visual Code Changes
- `_config.yaml` defaults - Added defaults for values in certain types of pages
	- Removed redundancies covered by defaults from template files

### Visual Code Changes
- `important.html` edits
	- Made `_includes/important-format.html` to hold formatting for the important div
	- Added the event URL to the important header
	- Refactored code to be shorter and maybe a little more efficient
	- Separated visual logic from event seeking logic

### Content Changes
* Removing files
	- Removed `irc/`
	- Renamed `archive.md` , and `template_event.md` to hide from output
* Adding HFOSS to the projects list - Page can be viewed at https://a1liu.github.io/bugs-nyu.github.io/projects/
* Added a 404 Not Found Page - Page can be viewed at https://a1liu.github.io/bugs-nyu.github.io/404.html

### Misc Changes
* `.github` folder
	- Moved `CONTRIBUTE.md` to `.github` and renamed it to `CONTRIBUTING.md`
	- Moved `README.md`, `LICENSE` and `CODEOWNERS` to `.github` as well
	- `.github/ISSUE_TEMPLATE` - Added issue templates
	- `.github/PULL_REQUEST_TEMPLATE` - Added a pull request template
