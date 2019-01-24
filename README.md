# Mithril ZeroFrame Router

This will allow you to use Mithril.js's built-in router
seamlessly on a ZeroNet website. Inspired by @krixano's
[vue-zeroframe-router](https://github.com/krixano/ZeroFrame-Router).

## Installation

TODO. Hopefully soon just `npm install --save
mithril-zeroframe-router`. For now just import the
`mithril-zeroframe-router.ts` file into your repository

## Usage

Import the `Resolver` object from `mithril-zeroframe-router`:

```
import Resolver from './mithril-zeroframe-router'
```

Ensure you have
[ZeroFrame](https://zeronet.io/docs/site_development/zeroframe_api_reference/)
imported and can make calls to it. Example if using the
`zeroframe` npm package:

```
import ZeroFrame from 'zeroframe'
const zeroframe = new ZeroFrame()
```

Now imagine you have the following `m.route` configuration:

```
m.route(document.body, '/', {
    '/': Main,
    '/blog': Blog,
})
```

Which means the default component shown is Main, and if you
navigate to `/blog` the Blog component is shown.

This is how it works on a normal website. If we wanted to convert
this to working with ZeroNet, all we need to do is the following:

```
// Informs Mithril of the URL hash on page load
zeroframe.cmd('wrapperInnerLoaded', [])

// Wrap all components in the Resolver function
m.route(document.body, '/', {
    '/': Resolver(Main),
    '/hello': Resolver(Hello),
})
```

Route changes will now be reflected in the address bar, and
opening `http://127.0.0.1:43110/1mysitehash/#!/blog` will now go
to the correct place (the Blog compoennt) instead of the default
route.

You can see an example of the router in use in the [Mithril ZeroNet
Template](https://github.com/anoadragon453/ZeroNet-Site-Template-Mithril)
repository.
