---
title: Making API calls to blitz.js from a react-native mobile app
description: A fix for trying to call blitz.js endpoints from a react native app that don't require a CSRF token saying that the CSRF token is invalid
publishDate: "24 Mar 2023"
tags: ["Software"]
---

There can be many issues when adapting an API produced by a tool like blitz.js to be used by other platforms with different needs. I'm writing this gist to document the issues I faced when trying to signup users using a blitz.js mutation API call.
Essentially my issue was that the API call seemed to want a CSRF token but how do you get a CSRF token when the request to get one requires one? Well as blitz.js validates **ALL CSRF token headers whether they are required or not to be validated**. This was an issue because by default `react-native` stores all `Set-cookie` response headers and passes those cookies along with all future requests.
Which was causing blitz.js to validate invalid credentials and throw a `CSRFMismatch` error even though those credentials where not required.

### Implementing the fix

The actual implementation of the fix for this issue is pretty simple if you are using `fetch` inside of your `react-native` app just pass the property `credentials: "omit"` or with a library like `axios` you can add the property `withCredentials: false` you should be able to find documentation for this for whatever library you are using to make your API requests. These properties tell the underlying react native libraries to not send credentials with these API requests.

## Conclusion

So this was a good few hours of my life... This feature of `react-native` feels a bit hand-fisted and underdeveloped. It seems like it could be useful if developed further but currently it feels more like an inconvenience.
