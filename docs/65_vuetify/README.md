# Style your pages with Vuetify

Vuetify is on the top three list of the most well-known UI frameworks for Vue.

## Adding Vuetify to a project

### Manual steps

```bash
npm add vuetify
```

In the file where you create the Vue application, add the following code:

```js
import { createApp } from 'vue'
import App from './App.vue'

// Vuetify
import 'vuetify/styles'
import { createVuetify } from 'vuetify'
import * as components from 'vuetify/components'
import * as directives from 'vuetify/directives'

const vuetify = createVuetify({
  components,
  directives,
})

createApp(App).use(vuetify).mount('#app')
```

This will include all components and directives regardless of whether or not you are using them. 

### CDN

We recommend using the latest version of Vuetify 3 from jsdelivr. All components and styles are included.

`https://cdn.jsdelivr.net/npm/vuetify@3.1.10/dist/vuetify.min.css`

`https://cdn.jsdelivr.net/npm/vuetify@3.1.10/dist/vuetify.min.js`

```js
const { createApp } = Vue
const { createVuetify } = Vuetify

const vuetify = createVuetify()

const app = createApp()
app.use(vuetify).mount('#app')
```

## Implementing Vuetify

For now we will be using the [Vuetify documentation website](https://vuetifyjs.com/en/getting-started/installation/) as a base of information to implement style with Vuetify to our Vue applications.

![image](./images/image1.png)