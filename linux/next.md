# next

* Download: [Github](https://github.com/atlas-engineer/next)
* Manual: [Manual](https://github.com/atlas-engineer/next/blob/master/documents/MANUAL.org)

## Quickstart

* C-l: Load URL in tab
* M-l: Load URL in a new tab
* C-x b: Switch tab
* C-b: Backwards history
* C-f: Forwards history
* C-x C-c: Quit


## Search in page

* C-s s: Search for a Given Term: This command will place a red box next to every match on a given web-page.
* C-s n: Next match: This command will move the next match to the top of the browser screen.
* C-s p: Previous match: This command will move the previous match to the top of the browser screen.
* C-s k: Clear Search: Remove the read search boxes from the screen.

## Zoom

* C-x C-=: Increase size
* C-x C--: Decrease size
* C-x C-0: Restore defaults


## Jumping to links

* C-g: Go to link in current tab
* M-g: Create new tab with link, focus on new tab
* C-u M-g: Create new tab with link, keep focus on current tab

## Customize

* Add customizations to ~/.config/next/init.lisp.
* The first line of an init file should contain the following package declaration in order to modify Next-specific variables and functions: `(in-package :next)`

#### Keybindings

```lisp
;; Bind multiple keys in root-mode using the default scheme.
(define-key
  "C-x o" 'example
  "SPACE" 'scroll-page-down)

;; Bind in root-mode using the vi-normal scheme.
(define-key :scheme :vi-normal
  "C-x o" 'example
  "SPACE" 'scroll-page-down)

;; Bind in document-mode using the vi-normal scheme.
(define-key :mode document-mode :scheme :vi-normal
  "C-x C-c s" 'save-history)

;; Bind in current buffer's first mode.  This won't affect other buffers.
(define-key :keymap (getf (keymap-scheme
                           (first (modes (active-buffer *interface*))))
                          :emacs)
  "C-x C-c h" 'hello-local-world)
```

The following keys exist as special keys:

* C: Control
* S: Super (Windows key, Command Key)
* M: Meta (Alt key, Option Key)
* s: Shift key

#### Keymaps and key binding schemes

The currently active key binding scheme is selected by the current-key-scheme buffer slot.  When a key is hit, Next looks up the keymaps of the corresponding scheme for all active modes in the current buffer.

```lisp
(add-to-default-list 'vi-normal-mode 'buffer 'default-modes)
```




