123-menu.el
===========

Even though I've been using Emacs for years, I still have trouble
remembering a lot of the key combinations for commands that I
don't use all the time (e.g.: killing and yanking rectangles,
bookmarks, etc.). I think Lotus 1-2-3 for DOS had a remarkably cool
user interface in that the menus let you explore around and find
things if you were a newbie, but once you knew the key sequences,
you could become very fast with it. This is my attempt at doing
something like the Lotus 1-2-3 menu system for Emacs.

This elisp defines only the primitives for creating menus and not the menus
themselves. The nice thing about this is that the user is free to define
whatever menus and keybindings are most convenient for them.

Here's an example of how I use it in my .emacs:

```el
(require '123-menu)

(123-menu-defmenu marc-menu-root
  ("a" "[A]bbrev"    '123-menu-display-menu-marc-menu-abbrev)
  ("b" "[B]uffer"    '123-menu-display-menu-marc-menu-buffer)
  ("c" "[C]ode"      '123-menu-display-menu-marc-menu-code)
  ("e" "[E]val"      '123-menu-display-menu-marc-menu-eval)
  ("f" "[F]ile"      '123-menu-display-menu-marc-menu-file)
  ("m" "[M]arks"     '123-menu-display-menu-marc-menu-marks)
  ("r" "[R]ect"      '123-menu-display-menu-marc-menu-rect)
  ("s" "[S]earch"    '123-menu-display-menu-marc-menu-search)
  ("v" "[V]ersion"   '123-menu-display-menu-marc-menu-version)
  ("w" "[W]indow"    '123-menu-display-menu-marc-menu-window))

(123-menu-defmenu marc-menu-abbrev
  ("g" "[G]lobal"              'add-global-abbrev)
  ("m" "[M]ode-specific"       'add-mode-abbrev)
  ("i" "[I]nverse"             '123-menu-display-menu-marc-menu-abbrev-inverse))

(123-menu-defmenu marc-menu-abbrev-inverse
  ("g" "[G]lobal"              'inverse-add-global-abbrev)
  ("m" "[M]ode-specific"       'inverse-add-mode-abbrev))

(123-menu-defmenu marc-menu-buffer
  ("k" "[K]ill"                'kill-buffer)
  ("l" "[L]ist"                'list-buffers)
  ("r" "[R]ename"              'rename-buffer))

(123-menu-defmenu marc-menu-code
  ("c" "[C]omment region"      'comment-region)
  ("u" "[U]ncomment region"    'uncomment-region))

(123-menu-defmenu marc-menu-eval
  ("b" "[B]uffer"              'eval-buffer)
  ("l" "[L]ast sexp"           'eval-last-sexp)
  ("r" "[R]egion"              'eval-region))

(123-menu-defmenu marc-menu-file
  ("d" "[D]ired"               'dired)
  ("f" "[F]ind"                'find-file)
  ("i" "[I]nsert"              'insert-file)
  ("s" "[S]ave"                'save-buffer))

(123-menu-defmenu marc-menu-marks
  ("j" "[J]ump"                'bookmark-jump)
  ("s" "[S]et"                 'bookmark-set))

(123-menu-defmenu marc-menu-rect
  ("k" "[K]ill"                'kill-rectangle)
  ("y" "[Y]ank"                'yank-rectangle)
  ("o" "[O]pen"                'open-rectangle))

(123-menu-defmenu marc-menu-search
  ("i" "[I]ncremental"         'isearch-forward)
  ("o" "[O]ccur"               'occur))

(123-menu-defmenu marc-menu-version
  ("a" "[A]nnotate"            'vc-annotate)
  ("d" "[D]iff"                'vc-diff)
  ("l" "[L]og"                 'vc-print-log))

(123-menu-defmenu marc-menu-window
  ("1" "[1]window"             'delete-other-windows)
  ("o" "[O]ther"               'other-window)
  ("v" "[V]ert split"          'split-window-vertically)
  ("h" "[H]oriz split"         'split-window-horizontally))

(define-key global-map "C-xm" '123-menu-display-menu-marc-menu-root)
```

If you use this, let me know what you think and if you have any suggestions for improvements.

