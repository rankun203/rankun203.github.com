title: Mongoose notes
date: 2015-08-25 22:57:08
categories:
- node.js
- note
tags:
- node.js
- mongoose
- note
---

## Custom getters

Use custom getters to process the MongoDB retunred data, like an interceptor.

Schema custom getters doesn’t work with lean().

Set up the Schema:

```javascript
DBSchema.set('toObject', {getters: true, virtuals: true});
DBSchema.set('toJSON', {getters: true, virtuals: true});
```

Add custom get function on specified field:

```javascript
DBSchema.path('images').get(function (images) {
  if (images && Array.isArray(images) && images.length > 0) {
    images = images.map(function (image) {
      return getUrl(image);
    });
  }
  return images;
});
```

<!-- more -->