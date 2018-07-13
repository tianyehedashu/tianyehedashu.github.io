---
title: istanbul 结合 mocha 生成 coverage
date: 2018-07-10 17:13:09
tags: istanbul/nyc,mocha, cros, env, bable
---

## Quick start
```bash
 npm  install --save-dev nyc
 npm  install --save-dev istanbul 
```
and add fellow code to you package.json
```JSON
{
  "scripts": {
    "cover": "nyc --reporter=lcov --reporter=text-lcov mocha"
  }
}
```
now you can run test by:

```bash
npm run cover 
```

## ES6支持 
### 安装 转换和配置相关的包
  ```bash
  npm install --save-dev babel-plugin-istanbul
  npm install --save-dev cross-env
  npm install --save-dev @babel/register
  npm install --save-dev babel-plugin-transform-runtim
  npm install --save-dev babel-preset-env
  npm install --save-dev babel-register
  ```

### 增加相关配置
增加如下代码到.bablerc
```JSON
  {
    "babel": {
      "presets": ["@babel/env"],
      "env": {
        "test": {
          "plugins": ["istanbul"]
        }
      }
    }
  }
```
增加下面代码到package.json
```JSON
{
  "nyc": {
    "require": [
      "@babel/register"
    ],
    "reporter": [
      "lcov",
      "text",
      "html"
    ],
    "sourceMap": false,
    "instrument": false
  },
  "scripts": {
    "test": "cross-env NODE_ENV=test nyc mocha"
  }
}
```
## 遇到的问题
1. mocha 要等所有打开的资源关闭后才能结束，就算case已经跑完，mocha 不结束，nyc就不能够生成报告.
2. mocha case报错也不能生成报告.
3. mocha 中如果使用了异步方法，那么2s后异步方法没有完成，case自动失败，通过如下配置 延长超时时间
   ```JSON
    "scripts": { 
        "cover": "cross-env NODE_ENV=covertest nyc   mocha --timeout=5000" 
    }
    ```
4. 如果你的NODE_ENV不是test，那么需要在.bablerc中增加对应的配置
如下：
    ```JSON
    "env": {
            "covertest": {
                "plugins": [
                    [
                        "istanbul"
                    ],
                    [
                        "transform-runtime",
                        {
                            "helpers": false,
                            "polyfill": false,
                            "regenerator": true,
                            "moduleName": "babel-runtime"
                        }

                    ]
                ]
            }
    }
    ```

### relactive link  
1. [istanbul with mocha](https://istanbul.js.org/docs/tutorials/mocha/)  
2. [nyc git hub](https://github.com/istanbuljs/nyc)
{% fi /images/timg.jpg %}