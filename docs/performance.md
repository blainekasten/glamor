performance considerations
---

When used plainly, glamor is fast and efficient enough for most sites. However, you can squeeze out more power by following some guidelines - 


- by far the biggest performance boost you can get is by compiling your code with `NODE_ENV=production` in conjunction with webpack's DefinePlugin / browserify's envify, etc. This triggers glamor to internally use `insertRule` instead of `appendChild` for adding styles to the stylesheet. You can optionally toggle this manually by calling `speedy(true/false)`
- by [server rendering your html AND css](https://github.com/threepointone/glamor/blob/master/docs/server.md), you can prepopulate / rehydrate some values when the page loads up, preventing fresh inserts on booting. This makes initial page load speed *much* faster. 
- we can also lean on [glamor's WeakMap caches](https://twitter.com/i/notifications) by using 'static' / predefined objects as arguments, instead of passing fresh objects every time. You can automate some of this bhavior by including `glamor/babel-hoist` to your babel plugin list
