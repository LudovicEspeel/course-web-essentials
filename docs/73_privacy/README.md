# Privacy

Let's talk about the privacy of the users of your website.

![image](./images/image2.png)

## legislation

Let's first watch [this video](https://www.youtube.com/watch?v=QWw7Wd2gUJk) to better understand the problem with cookies.

### GDPR

Companies have the right to process users' personal data if they have received permission or if they have a legitimate interest (e.g. to prevent fraud).

### ePrivacy Regulation

This is an extension of the GDPR legislation that will come into force soon:

* do not prohibit access to websites if the use of cookies has not been approved
* wifi location and device tracking
* privacy setting of the browsers by default
* regulation of the content of the metadata (cookies)

### Classification

Cookies fall under the following classification:

#### Duration

* session cookies: temporary and disappear when you close the browser
* persistent cookies: all other cookies => maximum 12 months according to ePrivacy Directive

#### Provenance

* first-party cookies: the cookies placed by the website you visit
* third-party cookies: these placed by a third party such as an advertiser (ads) or an analytic system

#### Purpose

* strictly necessary cookies: for example to log in, shopping cart contents
* preference cookies (functionality cookies): choices such as language, username and automatic login
* statistics cookies (performance cookies): counters, how the website was used, ... But made anonymous, can no longer be traced back to a person
* marketing cookies: track your online activity and help advertisers to target their advertising, usually third-party and persistent

### Cookie guidelines

* users must give permission before using cookies, except for the necessary cookies (strictly necessary cookies)
* informing the user exactly what data each cookie tracks, and this before consent is obtained
* document and store user consents
* allow users to use your service, even if they did not consent to certain cookies
* giving users the option to withdraw their consent

This is an nice example:

![image](./images/image1.png)

## Cookie consent

For this we will be using the internationalized [Cookie Consent component](https://www.npmjs.com/package/@avensio/cookie-consent?activeTab=readme) for vue 3.

Example:

```vue
<script setup>
import '@avensio/cookie-consent/style.css'
import CookieConsent from '@avensio/cookie-consent'

const obj = {
  requiredLinks: {
    privacy: {
      title: 'Privacy',
      href: '/privacy'
    },
    impress: {
      title: 'Imprint',
      href: '/imprint'
    }
  },
  categories: [
    {
      id: 'essential',
      label: 'Essential',
      description: 'Essential Cookies are needed for the website to function properly.',
      cookies: [
        {
          id: 'session-cookie',
          name: 'Session Cookie',
          provider: 'Owner of the Website',
          purpose: 'Saves as anynomous user the items in the shopping card and as authenticated user also additional infos',
          cookieName: 'SESSION',
          cookieValidityPeriod: '2 hours'
        }
      ]
    }
  ]
}
</script>

<template>
  <CookieConsent :categories="obj.categories" :required-links="obj.requiredLinks" />
</template>
```

## Cookie

A cookie is a small block of data (up to 4096 bytes) that the server sends to the client browser with the first HTTP Response. This client browser will send this cookie to the server with every subsequent HTTP request.

Initially, this was designed to keep track of who you are and what's in your shopping cart.

When the cookie is created, it is given a **name**, a **value** and an **expiration date** (number of seconds from 1970).

### Example


Here we will be using [vue3-cookies](https://www.npmjs.com/package/vue3-cookies?activeTab=readme) for handling browser cookies.

First install it with

```bash
npm install vue3-cookies
```

Next in your vue project import it

```vue
import VueCookies from 'vue3-cookies'
```

Then use it

```vue
<!-- without default settings -->
app.use(VueCookies);
<!-- with default settings -->
app.use(VueCookies, {
    expireTimes: "30d",
    path: "/",
    domain: "",
    secure: true,
    sameSite: "None"
});
```

Next you can use this

```vue
<!-- set a global cookie -->
this.$cookies.set('theme','default');
<!-- set a cookie -->
$cookies.set(keyName, value[, expireTimes[, path[, domain[, secure[, sameSite]]]]])
<!-- get a cookie -->
$cookies.get(keyName)
<!-- remove a cookie -->
$cookies.remove(keyName [, path [, domain]])
<!-- check if a cookie exists -->
$cookies.isKey(keyName)
```


