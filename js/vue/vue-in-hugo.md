---
title: Embeded Vue in Hugo Site
nav: vue in hugo
keywords: [vue, hugo]
vue: true
---


<div id='sample-app'>
    {{message}}
    <ul>
        <li v-for="i in fruit">
            {{ i }}
        </li>
    </ul>
</div>

<script>
    var app = new Vue({
        el: '#sample-app',
        data: {
            message: 'Hello Vue!',
            fruit: ['apple', 'banana', 'pear', 'orange']
        }
    })
</script>

```html
<div id='sample-app'>
    {{message}}
    <ul>
        <li v-for="i in fruit">
            {{ i }}
        </li>
    </ul>
</div>

<script>
    var app = new Vue({
        el: '#sample-app',
        data: {
            message: 'Hello Vue!',
            fruit: ['apple', 'banana', 'pear', 'orange']
        }
    })
</script>
```
