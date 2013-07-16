org-trello
==========

[![Build Status](https://travis-ci.org/ardumont/org-trello.png?branch=master)](https://travis-ci.org/ardumont/org-trello)

Sync your org-mode files with your trello boards.

# why?

- org-mode is what I need.
- Trello is what my team need.
- org-trello may satisfy everybody.

# Contributions

Pull Requests welcome
cf. [What has been done and remains to be done](./TODO.org)

# Release notes

## Details

[todo/done](./TODO.org)

## v0.0.4

- DONE Permit the user to deal with his/her own trello list (based on his/her org-mode keywords - cf. http://orgmode.org/manual/In_002dbuffer-settings.html)
- DONE Deploy on marmalade the stable version (and update the readme about it)
- DONE Rewrite tests using `expectations`
- DONE Simplify some code regarding destructuring for example
- DONE Remove useless code
- DONE Improve documentations and sync the routine check message with the documentation.
- DONE Update documentation

## v0.0.3

- DONE Syncing complex entities
- DONE cleanup useless tests
- DONE Namespace cleanup
- DONE Building package is now able to deal with the right version
- DONE Create a board from org-mode
- DONE Display the name of the board as a property file
- DONE Cleanup the useless controls
- DONE Given a org-mode file, fill in the trello board
- DONE Announce in emacs mailing list
- DONE Filter out the closed boards from the "choose board list"
- DONE filter out level > 4 when syncing.
- DONE Given a trello board, sync into a org-mode file
- cf. [todo/done](./TODO.org) for the remains

## v0.0.2

- Technical release fixing technical details
- Fixing the packaging (inlining into org-trello.el)
- Adding ci-travis
- Local packaging to help testing

## v0.0.1

- write only mode at the moment (org-mode pushes to trello, no reading yet)
- simple entity creation (card, checklist, item/task), the request is asynchroneous
- entity deletion (card, checklist, item/task)
- Interactive command to ease the setup of the consumer-key and the access-token
- Interactive command to ease the setup of one org-mode file (which represents one trello board). I assume there exists
  a 'todo', 'doing', and 'done' list (named that way too)
- Control that the setup file (consumer-key and access-token) are rightly generated (to avoid later problem)
- Control that the properties on the current org-mode file are rightly setuped to access a trello board
- packaging for melpa

# Install

## marmalade - Stable version

Add this to your emacs's init file (~/.emacs, ~/.emacs.d/init.el, or *scratch*, or whatnot...)

``` lisp
(require 'package)

(add-to-list 'package-archives '("melpa" . "http://melpa.milkbox.net/packages/") t)

(package-initialize)
```
Then hit, `M-x eval-buffer` to evaluate the contents.

## melpa - ~snapshot

Add this to your emacs's init file (~/.emacs, ~/.emacs.d/init.el, or *scratch*, or whatnot...)

``` lisp
(require 'package)

(add-to-list 'package-archives '("marmalade" . "http://marmalade-repo.org/packages/"))

(package-initialize)
```
Then hit, `M-x eval-buffer` to evaluate the contents.

## org-trello

You can install org-trello:

``` lisp
(when (not package-archive-contents)
  (package-refresh-contents))

;; Add in your own as you wish:
(defvar my-packages '(org-trello)
  "A list of packages to ensure are installed at launch.")

(dolist (p my-packages)
  (when (not (package-installed-p p))
    (package-install p)))
```

Again, hit `M-x eval-buffer`.

## github

Download org-trello from GitHub

```sh
git clone http://github.com/ardumont/org-trello.git
```

Add the org-trello directory to your load path and then add

``` lisp
(add-to-list 'load-path "/path/to/org-trello/"))
(require 'org-trello)
```

## Example

- [Adding emacs repository](https://github.com/ardumont/install-packages-pack/blob/master/init.el)
- [Installing org-trello](https://github.com/ardumont/orgmode-pack/blob/master/init.el#L1)

# Setup

## Emacs related

Orgtrello is a minor mode for org-mode to sync.
Simply, require it somewhere on your load file (~/.emacs or ~/.emacs.d/init.el).

``` lisp
(require 'orgtrello)
```

For example, here is my [startup file](https://github.com/ardumont/orgmode-pack/blob/master/init.el#L3).

## Trello related

### keys

Install the consumer-key and the read-write token for org-trello to be able to work in your name with your trello boards.

`C-c o i`

or

``` lisp
M-x org-trello/install-key-and-token
```

### Sync org to trello

#### pre-requisite

Beware, this step implicitely requires you to prepare your trello board by creating the needed list (in accordance to your org-mode keywords, cf. [org-todo-keywords](http://orgmode.org/manual/In_002dbuffer-settings.html)).

For example, I use the following keywords:

```lisp
(setq org-todo-keywords
   '((sequence "TODO" "IN-PROGRESS" "PENDING" "|"  "DONE" "FAIL" "DELEGATED" "CANCELLED")))
```
This is one way to setup org-mode, this can also be done on a org-mode file basis (cf. [previous link](http://orgmode.org/manual/In_002dbuffer-settings.html))

As a consequence, I need to create the list "TODO", "IN-PROGRESS", "PENDING", "DONE", "FAIL", "DELEGATED", and "CANCELLED" in my trello board before.

#### Sync

For each org-mode file, you need to connect your org-mode file with a trello board.

`C-c o I`

or

``` lisp
M-x org-trello/install-board-and-lists-ids
```

A simpler way would be to...

### Create a board

You can avoid the previous step and create directly a board from your org-mode file.
This will create the list from the keywords you use in your org-mode (cf. [org-todo-keywords](http://orgmode.org/manual/In_002dbuffer-settings.html)).

`C-c o b`

or

``` lisp
M-x org-trello/create-board
```

# Bindings

Actual bindings (not definitive, suggestions regarding those bindings are welcome):
- C-c o i - Interactive command to install the key and the read/write access-token.
- C-c o I - Interactive command to setup your org-mode file to work with your remote trello board
- C-c o b - Create interactively a board and attach the org-mode file to this trello board.
- C-c o c - Create/Update asynchronously an entity (card/checklist/item) depending on its level and status. Do not deal with level superior to 4.
- C-c o C - Create/Update a complete entity card/checklist/item and its subtree (depending on its level).
- C-c o s - Synchronize the org-mode file to the trello board (org-mode -> trello).
- C-c o S - Synchronize the org-mode file from the trello board (trello -> org-mode).
- C-c o k - Kill the entity (and its arborescence tree).
- C-c o h - This help message.

# Use cases

1. open an org-mode file

2. Install the key and the token file (`C-c o i` or `M-x org-trello/install-key-and-token`).
This will open your browser to retrieve the needed informations (`consumer-key` then the `access-token`) and wait for your input in emacs.
*Remark:* This need to done once and for all time until you revoke such token.

3. Setup your org-mode file with your trello board (`C-c o I` or `M-x org-trello/install-board-and-lists-ids`).
This will present you a list of your actual boards. Select the one you want and hit enter.
This will edit your org-mode file with properties needed.

*Remarks:*
- This need to be done once for each org-mode file you want to sync with a trello board.
- You can create directly a board (`C-c o b` or `M-x orgtrello/do-create-board-and-lists`)

4. Now you are ready to use org-mode as usual.

The idea is this:
- 3 levels:
  level 1 - Card
  level 2 - Checklist
  level 3 - Item

For example:

```org-mode
* card-identity
** checklist
*** task1
*** task2
*** task3
```

Creation step by step:
- Card:
  - Place yourself on the `card-identity` and hit the binding *BINDING-SIMPLE-CREATION*, this will create the card in the `TODO` column in your trello board
  - You can edit the title and hit *BINDING-SIMPLE-CREATION*, this will update the title in trello
  - Change the status from TODO to any intermediary status, then hit the binding, this will move the card to the list `DOING`.
  - Once done, move the status of the card from anything to DONE, hit the binding, this will move the card to the list `DONE`.
- Checklist:
  - Place yourself on the checklist `checklist`, hit the binding, this will add `checklist` as a checklist to your card `card-identity`
  - Rename your checklist and hit again the binding to update its label
- Task:
  - Place yourself on your task and hit *BINDING-SIMPLE-CREATION*, this will add the item to such checklist.
  - Change the name of the task and hit *BINDING-SIMPLE-CREATION*, this will update its label
  - Change the status of the task to `DONE` and hit the binding, this will check such item in trello.

5. You can sync all of the entity and its arborescence once:
Place yourself on the entity (card or checklist) and hit `C-c o C`.

At the moment, this action is synchonous.

6. You can sync all your org-mode file to trello too.
Hit `C-c o s`.

At the moment, this action is synchonous.

7. You can sync the content of your board into an org-mode file too.
Hit `C-c o S`.

At the moment, this action is synchronous.

8. You can remove the entity and its arborescence with `C-c o k`.

# Demo

- [Install](http://youtu.be/e3NzllAHbHY)
- [Setup key and token](http://youtu.be/ReUp1Wn5scc)
- [Attach org-mode file to one trello board](http://youtu.be/2PT8K1HG-eY)
- [Synchronize one entity](http://youtu.be/ILPs74L5LFU)
- [Synchronize one complete entity and move entity according to status](http://youtu.be/H8DXm5BLaD0)
- [Synchronize from org-mode file to trello](http://youtu.be/d6SATWzhQhs)
- [Synchronize from trello to org-mode files](http://youtu.be/-ldo8gvhaTY)
- [Create board and sync](http://youtu.be/6k4zRm6t8ZY)

# License

org-trello is free software under GPL v3. See COPYING file for details.
