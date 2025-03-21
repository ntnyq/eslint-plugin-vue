---
pageClass: rule-details
sidebarDepth: 0
title: vue/no-watch-after-await
description: disallow asynchronously registered `watch`
since: v7.0.0
---

# vue/no-watch-after-await

> disallow asynchronously registered `watch`

- :gear: This rule is included in all of `"plugin:vue/essential"`, `*.configs["flat/essential"]`, `"plugin:vue/strongly-recommended"`, `*.configs["flat/strongly-recommended"]`, `"plugin:vue/recommended"` and `*.configs["flat/recommended"]`.

## :book: Rule Details

This rule reports the `watch()` after `await` expression.  
In `setup()` function, `watch()` should be registered synchronously.

<eslint-code-block :rules="{'vue/no-watch-after-await': ['error']}">

```vue
<script>
import { watch } from 'vue'
export default {
  async setup() {
    /* ✓ GOOD */
    watch(watchSource, () => { /* ... */ })

    await doSomething()

    /* ✗ BAD */
    watch(watchSource, () => { /* ... */ })
  }
}
</script>
```

</eslint-code-block>

This rule is not reported when using the stop handle.

<eslint-code-block :rules="{'vue/no-watch-after-await': ['error']}">

```vue
<script>
import { watch } from 'vue'
export default {
  async setup() {
    await doSomething()

    /* ✓ GOOD */
    const stopHandle = watch(watchSource, () => { /* ... */ })

    // later
    stopHandle()
  }
}
</script>
```

</eslint-code-block>

## :wrench: Options

Nothing.

## :books: Further Reading

- [Guide - Reactivity - Computed and Watch](https://v3.vuejs.org/guide/reactivity-computed-watchers.html)
- [Vue RFCs - 0013-composition-api](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0013-composition-api.md)

## :rocket: Version

This rule was introduced in eslint-plugin-vue v7.0.0

## :mag: Implementation

- [Rule source](https://github.com/vuejs/eslint-plugin-vue/blob/master/lib/rules/no-watch-after-await.js)
- [Test source](https://github.com/vuejs/eslint-plugin-vue/blob/master/tests/lib/rules/no-watch-after-await.js)
