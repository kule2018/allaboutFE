Route对象

|   参数   |                   说明                    |  类型   | 默认值 |
| :------: | :---------------------------------------: | :-----: | :----: |
|  hidden  |        控制路由是否显示在 sidebar         | boolean | false  |
| redirect | 重定向地址, 访问这个路由时,自定进行重定向 | string  |        |
|   name   |       路由名称, 建议设置,且不能重名       | string  |        |
|   meta   |      路由元信息（路由附带扩展信息）       | object  |   {}   |

Meta路由元信息

|        参数         |                             说明                             |  类型   | 默认值 |
| :-----------------: | :----------------------------------------------------------: | :-----: | :----: |
|        title        |         路由标题, 用于显示面包屑, 页面标题 *推荐设置         | string  |        |
|        icon         |                    路由在menu上显示的图标                    | string  |        |
|      keepAlive      |                          缓存该路由                          | boolean | false  |
| hiddenHeaderContent |        *特殊 隐藏组件中的页面带的 面包屑和页面标题栏         | boolean | false  |
|     permission      | 与项目提供的权限拦截匹配的权限，如果不匹配，则会被禁止访问该路由页面 |  array  |   []   |

```javascript
 {
  path:'',
  component:''
  redirect: noredirect,
  name: 'router-name',
  hidden: true,
  meta: {
    title: 'title',
    icon: 'a-icon',
    keepAlive: true,
    hiddenHeaderContent: true,
  }
}
```

