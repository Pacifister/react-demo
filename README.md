该项目主要是[create-react-app](https://github.com/facebook/create-react-app)脚手架的一些配置和优化。
## 引入`antd`
1. 安装依赖
```
yarn add antd react-app-rewired babel-plugin-import react-app-rewire-less
```
2. 修改启动配置为 `react-app-rewired`
```json
/* package.json */
"script": {
	"start": "react-app-rewired start",
	"build": "react-app-rewired build",
	"test": "react-app-rewired test"
}
```
3. 新增配置文件`config-overrides.js`
```js
const { injectBabelPlugin } = require('react-app-rewired');
const rewireLess = require('react-app-rewire-less');

module.exports = function override(config, env) {
  config = injectBabelPlugin(
    ['import', { libraryName: 'antd', libraryDirectory: 'es', style: true }], // change importing css to less
    config
  );
  config = rewireLess.withLoaderOptions({
    modifyVars: { '@primary-color': '#1DA57A' },
    javascriptEnabled: true
  })(config, env);
  return config;
};

```
