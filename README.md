# vue-render-if

The `vue-render-if` component makes checking against data in your template, easy. This component helps clean up your Vue `template` by not writing `v-if`s everywhere and checking for multiple types of "falsy" type values.

__Before__

```html
<template>
  <div v-if="value1 !== '' && value1 !== undefined && value1 !== null && value2 !== undefined && value2 !== null && value3 !== undefined && value3 !== null">
    <p>I should only render if every value is not undefined, null, or an empty string.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value1: 'Vue.js',
      value2: true,
      value3: 2018
    }
  }
}
</script>
```

__After__

```html
<template>
  <render-if :defined="[value1, value, value3]">
    <p>I should only render if every value is not undefined, null, or an empty string.</p>
  </render-if>
</template>

<script>
import RenderIf from 'vue-render-if';

export default {
  components: {
    RenderIf,
  },
  data() {
    return {
      value1: 'Vue.js',
      value2: true,
      value3: 2018
    }
  }
}
</script>
```

By default, `vue-render-if` will render a `div` and will check if the values passed in the `defined` props array is either `undefined`, `null`, or an empty string `''`. You can however, define your own invalid values.

__Note:__ You can also pass in a single value if you are checking against one data or state property.

```html
<template>
  <render-if :defined="value1">
    <p>I should only render if every value is not undefined, null, or an empty string.</p>
  </render-if>
</template>
```

## Options

`vue-render-if` accepts three `props`, one of which is required (`defined`). The other two props are `tag` and `not-valid`.

| Prop Name | Required | Default Value | Accepts                             | Purpose                                                                                  |
|-----------|----------|---------------|-------------------------------------|------------------------------------------------------------------------------------------|
| defined   | yes      | N/A           | Array (all types) or a single value | List all of the data items that should have a value of some kind for the slot to render. |
| tag       | no       | 'div'         | String                              | Defines the HTML tag `render-if` should render as.                                       |
| not-valid | no       | N/A           | Array (all types) or a single value | Defines all of the property values that should be considered invalid.                    |


```html
<template>
  <render-if :defined="value1" tag="section" :not-valid="['foo, bar', undefined, null, '']">
    <p>I should only render if every value is not undefined, null, or an empty string.</p>
  </render-if>
</template>
```

This instance will...
- Render if `value1` is not `'foo'`, `'bar'`, `undefined`, `null, or empty.
- Render a `section` tag.

__Note:__ If you defined values for the `not-valid` prop, you will need to add `undefined`, `null`, and `''` if you still want those to be falsy.

## Usage

```bash
$ yarn add vue-render-if
# or
npm install --save vue-render-if
```

### Add it Globally

__main.ts__
```javascript
import RenderIf from 'vue-render-if';

Vue.component('render-if', RenderIf);
```

### Using it in a Vue Component
```html
<script>
import RenderIf from 'vue-render-if';

export default {
  components: {
    RenderIf
  }
}
</script>
```

## Contributing
1. Fork it!
2. Create your feature branch: git checkout -b my-new-feature
3. Commit your changes: git commit -am 'Add some feature'
4. Push to the branch: git push origin my-new-feature
5. Submit a pull request!

## Author

__vue-render-if__ © Dave Berning, Released under the MIT License.

[daveberning.io](https://daveberning.io) - [GitHub](https://github.com/daveberning) - [Twitter](https://twitter.com/daveberning)

Special thanks to Cory Kleiser, Lance Deters, and Craig Mullin.