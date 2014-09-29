# Javascript Coding Standard

> **TEAM**: This document is taken from Github. Please use or remove it.

## Style Guide

- No trailing semicolons.
- No trailing whitespace.
- Keep lines fewer than 120 characters.
- Always include a space before and after a function arrow.

```javascript
# bad
sum = (a,b)->a + b
# good
sum = (a,b) -> a + b
```

- No empty parameter lists

```javascript
# bad
$el.on 'click', ->
  $.get(url).then =>
    console.log "this is never used"
```

- Cyclomatic complexity must not exceed 38 per file. TODO: Work on lower this to something saner.
- Always throw Errors, not strings.

```javascript
# bad
throw "expected string, got number"

# good
throw new TypeError "expected string, got number"
```

## Linting

[CoffeeLint](http://www.coffeelint.org/) is used to enforce these coding styles. Many of the default configuration options are used. Here are the options we are overriding.

```javascript
{
  "arrow_spacing": {
    "name": "arrow_spacing",
    "level": "error"
  },
  "max_line_length": {
    "name": "max_line_length",
    "value": 120,
    "level": "error",
    "limitComments": true
  },
  "indentation": {
    "name": "indentation",
    "value": 2,
    "level": "ignore"
  },
  "no_empty_param_list": {
    "name": "no_empty_param_list",
    "level": "error"
  },
  "cyclomatic_complexity": {
    "name": "cyclomatic_complexity",
    "value": 22,
    "level": "error"
  },
  "no_unnecessary_fat_arrows": {
    "name": "no_unnecessary_fat_arrows",
    "level": "error"
  }
}
```