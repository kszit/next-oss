.next files generated by NEXT packaging are uploaded to the cloud to improve the loading speed of NEXT framework resources

## Install
```bash
npm install next-oss cross-env --save-dev
```

## Compatibility
### Node
Node.js >= 10.10.0 required

## How to use

### Init Cloud
Currently, only `aliyun` is supported. Based on `ali-oss` module  
Create `oss.js` in the project root directory, this code
```jsx
const NextOSS = require("next-oss");
const {method} = process.env;


// init aliyun
NextOSS.initAliyun({
  region: '<oss region>',
  accessKeyId: '<Your accessKeyId>',
  accessKeySecret: '<Your accessKeySecret>',
  bucket: '<Your bucket name>'
});

let options = {
  folder: "<cloud folder>",
  dirname: __dirname,
};

NextOSS.config(options);


if(method === "upload"){
  NextOSS.upload();     // upload
} else if(method === "remove"){
  NextOSS.remove();     // delete previous versions
}
```
#### Supported options by NextOSS.config:
- `folder` - A directory saved to the cloud, is request
- `dirname` - You need to pass in `_dirname` to get the `.next` folder, is request
- `log` - Whether to print logs, default false

### Add Scripts
and add a script to your package.json like this:
```json
{
  "scripts": {
    "upload": "cross-env method=upload node oss.js",
    "remove": "cross-env method=remove node oss.js"
  }
}
```

### upload
```bash
npm run upload
```

### remove
```bash
npm run remove
```



