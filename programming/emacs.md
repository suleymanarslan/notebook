# Emacs

Debugging:

```
pkill -USR2 emacs 
```


## `eval-expression`

Shortcut: `M-:`

## `describe-font`

It shows font is being used.

## `describe-key`

It shows the description of a binding.

Shortcut: C-h k

## `describe-function`

It shows the keybinding(s) of the function

Shortcut: C-h f

## interactive `eval-expression`

Shortcut: `M-:`

## List available fonts

Evaluate:

```elisp
(font-family-list)
```

## Dap Mode 

Template for running a test:

```elisp
(dap-register-debug-template
  "Launch Test"
  (list :type "go"
        :request "launch"
        :name "Launch File"
        :mode "auto"
	      :program "/home/azer/Projects/__/__/____test.go"
        :buildFlags nil
        :args nil
      	:env '(("ENV_FILE" . "/home/azer/Projects/___/.env"))
        :envFile nil))
```
