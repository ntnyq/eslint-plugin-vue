---
pageClass: rule-details
sidebarDepth: 0
title: vue/valid-v-if
description: enforce valid `v-if` directives
since: v3.11.0
---

# vue/valid-v-if

> enforce valid `v-if` directives

- :gear: This rule is included in all of `"plugin:vue/essential"`, `*.configs["flat/essential"]`, `"plugin:vue/vue2-essential"`, `*.configs["flat/vue2-essential"]`, `"plugin:vue/strongly-recommended"`, `*.configs["flat/strongly-recommended"]`, `"plugin:vue/vue2-strongly-recommended"`, `*.configs["flat/vue2-strongly-recommended"]`, `"plugin:vue/recommended"`, `*.configs["flat/recommended"]`, `"plugin:vue/vue2-recommended"` and `*.configs["flat/vue2-recommended"]`.

This rule checks whether every `v-if` directive is valid.

## :book: Rule Details

This rule reports `v-if` directives in the following cases:

- The directive has that argument. E.g. `<div v-if:aaa="foo"></div>`
- The directive has that modifier. E.g. `<div v-if.bbb="foo"></div>`
- The directive does not have that attribute value. E.g. `<div v-if></div>`
- The directive is on the elements which have `v-else`/`v-else-if` directives. E.g. `<div v-else v-if="foo"></div>`

<eslint-code-block :rules="{'vue/valid-v-if': ['error']}">

```vue
<template>
  <!-- ✓ GOOD -->
  <div v-if="foo" />
  <div v-else-if="bar" />
  <div v-else />

  <!-- ✗ BAD -->
  <div v-if />
  <div v-if:aaa="foo" />
  <div v-if.bbb="foo" />
  <div
    v-if="foo"
    v-else
  />
  <div
    v-if="foo"
    v-else-if="bar"
  />
</template>
```

</eslint-code-block>

::: warning Note
This rule does not check syntax errors in directives because it's checked by [vue/no-parsing-error] rule.
:::

## :wrench: Options

Nothing.

## :couple: Related Rules

- [vue/valid-v-else]
- [vue/valid-v-else-if]
- [vue/no-parsing-error]

[vue/valid-v-else]: ./valid-v-else.md
[vue/valid-v-else-if]: ./valid-v-else-if.md
[vue/no-parsing-error]: ./no-parsing-error.md

## :rocket: Version

This rule was introduced in eslint-plugin-vue v3.11.0

## :mag: Implementation

- [Rule source](https://github.com/vuejs/eslint-plugin-vue/blob/master/lib/rules/valid-v-if.js)
- [Test source](https://github.com/vuejs/eslint-plugin-vue/blob/master/tests/lib/rules/valid-v-if.js)
