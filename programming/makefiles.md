# Makefiles

## Defining Variables

```make
$(eval missingPackages := `grep -oFf /tmp/.snt-go-pkgs Gopkg.lock`)
```

## Conditions

```make
@if [ "$(missingPackages)" = "" ]; then\
  echo "Gopkg.lock looks good.";\
else \
  echo "Gopkg.lock is missing $(missingPackages)"; \
  exit 1;\
fi
```

## Multiline strings

It's possible as long as the variable is exported

```make
export COMPONENT_HTML
create-component:
  define COMPONENT_HTML
import html from "choo/html"

const view = (state, prev, send) => html`
$(name)
`

export default view
```
  endef

  @echo "$$COMPONENT_HTML" > ui/components/${name}.js
