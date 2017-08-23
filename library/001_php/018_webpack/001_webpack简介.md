# webpack
[webpack翻译文档：http://www.jianshu.com/p/cd123afa196a](http://www.jianshu.com/p/cd123afa196a);
## 安装
`npm install -g [--save-dev] webpack `<br>
`npm install -g [--save-dev] webpack-dev-server `

## 配置
- 项目配置文件 package.json
```javascript
{
  "name": "",
  "version": "1.0.0",
  "main": "",
  "license": "MIT",
  "dependencies": {   //--save
    "babel-core": "^6.18.2",
    "babel-loader": "^6.2.8",//编译器可以将es6语法转成低版本[如es5语法]提高兼容性,可以将JSX / ES6文件转换为JS文件
    "babel-preset-es2015": "^6.18.0",//使用babel-loader时对 ES6和React进行transpile(转义)需要用此插件
    "babel-preset-react": "^6.16.0",//使用babel-loader时对 ES6和React进行transpile(转义)需要用此插件
    "body-parser": "^1.15.2",
    "react": "^15.4.1",
    "react-dom": "^15.4.1",
    "react-redux": "^4.4.6",
    "redux": "^3.6.0",
    "webpack": "^1.14.0"
  },
  "devDependencies": {  //--save-dev 开发所需
    "antd": "^2.10.4"
  }
}
```

- webpack配置文件 webpack.config.js
```javascript
const webpack = require('webpack');
module.exports = {
  entry: {
    login: './dev/login.jsx',
    register: './dev/register.jsx',
    admin: './dev/admin.jsx'
  },
  output: {
    path: './static/js/admin/',
    filename: '[name].js'
  },
  module: {
    loaders: [{
      test: /\.js[x]?$/,
      exclude: /node_modules/,
      loader: 'babel-loader?presets[]=es2015&presets[]=react'
    }]
  },
  plugins: [
    // new webpack.DefinePlugin({
    //   'process.env': {
    //     'NODE_ENV': JSON.stringify('production')
    //   }
    // }),
    // 压缩插件(一般只在生产环境启用，服务器端还可以开启 gzip 压缩，优化的效果更明显)
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      }
    })
    // new webpack.SourceMapDevToolPlugin({
    //   // Match assets just like for loaders.
    //   test: string | RegExp | Array,
    //   include: string | RegExp | Array,
    //
    //   // `exclude` matches file names, not package names!
    //   exclude: string | RegExp | Array,
    //
    //   // If filename is set, output to this file.
    //   // See `sourceMapFileName`.
    //   filename: string,
    //
    //   // This line is appended to the original asset processed. For
    //   // instance '[url]' would get replaced with an url to the
    //   // sourcemap.
    //   append: false | string,
    //
    //   // See `devtoolModuleFilenameTemplate` for specifics.
    //   moduleFilenameTemplate: string,
    //   fallbackModuleFilenameTemplate: string,
    //
    //   module: bool, // If false, separate sourcemaps aren't generated.
    //   columns: bool, // If false, column mappings are ignored.
    //
    //   // Use simpler line to line mappings for the matched modules.
    //   lineToLine: bool | {test, include, exclude}
    // })
  ]
};
```
