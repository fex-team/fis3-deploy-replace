# fis3-deploy-replace
fis3-deploy-replace


## INSTALL

```bash
npm install [-g] fis3-deploy-replace
```

## USE

```js
fis.match('**', {
    deploy: [
        fis.plugin('replace', {
            from: 'from/string',
            to: 'to/string'
        }),
        fis.plugin('local-deliver') //must add a deliver, such as http-push, local-deliver
    ]
});
```
