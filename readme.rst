
################
Counsel at Point
################

This is a simple package to improve on the ergonomics for counsel by:

- Searching from the project root.
- Using the current context to initialize the search.
- Activating the current item in the search results.

An example of this is ``counsel-at-point-git-grep`` (matching ``counsel-git-grep``)
which initializes the search using the word at the cursor or the selection (if one exists).
The current line will be selected when prompted to select an item.

This makes it very quick to jump to other instances of text in a project without having to check if they happen
to be the instance you're already looking at.

Available via `melpa <https://melpa.org/#/counsel-at-point>`__.


Motivation
==========

While the tweaks to counsel this package provides are minor,
searching for text in a project is something done so often that even small changes are worth taking advantage of.


Usage
=====

This package doesn't modify counsel behavior, instead it provides commands that behave differently.

There is no minor mode, just commands you can configure emacs to use.


Commands
--------

Search File Contents (``counsel-at-point-git-grep``, ``counsel-at-point-ag``, ``counsel-at-point-rg``)
   Search using counsel commands with matching names (``counsel-git-grep``... etc).

   - Search from the projects root.
   - Initializes the search with text at the cursor.
   - Pre-select the current buffer & line number.

Search File Names (``counsel-at-point-file-jump``, ``counsel-at-point-find-file``, ``counsel-at-point-fzf``)
   Search file names using counsel commands with matching names (``counsel-file-jump``... etc).

   - Search from the projects root.
   - Pre-select the file name of the current buffer.

Search Buffer Contents (``counsel-at-point-grep``)
   Search in the current buffer using ``counsel-grep``.

   - Initializes the search with text at the cursor.
   - Pre-select the current line number.

IMenu (``counsel-at-point-imenu``)
   Select an IMenu item using ``counsel-imenu``.

   - Pre-select the nearest item at or before the current line.


Customization
-------------

``counsel-at-point-project-root`` (``'counsel-at-point-project-root-default``)
   Find the projects root-directory from the current buffer.
   This callback takes no arguments and must return a string or nil.

   The default functions uses ``find-file-in-project``, ``projectile``, ``project`` when available,
   falling back to version-control and finally ``default-directory`` if all other methods fail.

``counsel-at-point-thing-at-point`` (``'symbol-at-point``)
   The function to return text to initialize the search (when searching text contents).

   You may prefer to set this to ``'word-at-point`` for example.


Installation
============

The package is available in melpa as ``counsel-at-point``, here is an example with ``use-package``:

.. code-block:: elisp

   (use-package counsel-at-point
     :commands (counsel-at-point-file-jump
                counsel-at-point-git-grep
                counsel-at-point-imenu))

   ;; Example key bindings.
   (define-key prog-mode-map (kbd "M-n") 'counsel-at-point-git-grep)
   (define-key prog-mode-map (kbd "M-o") 'counsel-at-point-imenu)
   (define-key prog-mode-map (kbd "M-p") 'counsel-at-point-file-jump)
