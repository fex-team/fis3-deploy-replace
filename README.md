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


## EXAMPLE

多字符串替换

```js
fis.match('**', {
    deploy: [
        fis.plugin('replace', {
            from: /(img|cdn)\.baidu\.com/,
            to: function ($0, $1) {
                switch ($1) {
                    case 'img':
                        return '127.0.0.1:8080';
                    case 'cdn':
                        return '127.0.0.1:8081';
                }
                return $0;
            }
        }),
        fis.plugin('local-deliver')
    ]
});
```

或者

```js
function replacer(opt) {
    if (!Array.isArray(opt)) {
        opt = [opt];
    }
    var r = [];
    opt.forEach(function (raw) {
        r.push(fis.plugin('replace', raw));
    });
    return r;
};

fis.match('*', {
    deploy: replacer([
        {
            from: 'a',
            to: 'b',
        },
        {
            from: 'a0',
            to: 'b0'
        }
    ]).concat(fis.plugin('local-deliver'));
});
```

机智的你可能已经发现了点什么。我们配置了多个功能单一的 `fis.plugin('replace')`。