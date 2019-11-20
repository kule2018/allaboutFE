#### import xxx from ‘@/xxx’中@的作用

```javascript
module.exports = {
  context: path.resolve(__dirname, './'),
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      '@': resolve('src'),
      '@views': resolve('src/views'),
      '@comp': resolve('src/components'),
      '@core': resolve('src/core'),
      '@utils': resolve('src/utils')
    }
  }
}

//在webpack.config.js文件中，可如上配置，@代表src路径。
```





























