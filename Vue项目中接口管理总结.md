### 注意：关于axios的封装， 根据自己的项目需求会有相应的不同操作。 以下阐述项目中遇到的方式和学习到的代码分类管理方法。

接口管理部分可设置在src文件下的api文件中，接口可单独设置module文件中，与配置相关的js文件与module同级。

![image-20191101170931053](C:\Users\henry\AppData\Roaming\Typora\typora-user-images\image-20191101170931053.png)![image-20191101171723162](C:\Users\henry\AppData\Roaming\Typora\typora-user-images\image-20191101171723162.png)

接口文件设置：

```javascript
const ***=[
    {
        name:'',
        url:'',
        method:'',
        meta:{
            title:'',
            host:
        }
    },
        {
        name:'',
        url:'',
        methods:'',
        meta:{
             title:''
             host:
                }
    }
]
export default ***
```

相关的配置文件：

```javascript
// axios封装库
import ApiCreator from '***/utils/apiCreator'
// 导入module中接口参数设置的全部模块
import xxx from './modules/***'
import xxx from './modules/***'

const modules = {
  xxx,
  xxx
}  

// 配置
const CONFIG = {
  // 根路径
  BASE: '',
  // 是否允许携带cookie，session等验证
  WITHCREDENTIALS: true,
  // 请求超时时间
  TIMEOUT: 30000,
  // 接口模块
  MODULES: modules,
  beforeRequest: (config) => {
    // 如果接口需要传递host，则加上host作为参数
    if (config.meta && config.meta.host) {
      // 看是什么请求
      const hostId = Store.state.app.currentHost.id
      if (config.method === 'get') {
        config.params.host = hostId
      } else {
        config.data += '&host=' + hostId
      }
    }
    return config
  },
  // 请求前错误处理回调
  requestError: () => {

  },
  // 请求后错误处理回调
  responseError: () => {

  }
}

const apiCreator = new ApiCreator(CONFIG)
const api = apiCreator.create()

export default api

```

其中关于axios的封装库（src->utils->apiCreator.js)：

```javascript
// 生成接口请求列表的模块，即插即用，可在入口文件处配置
// 配置和核心代码分离的设计逻辑
import Axios from 'axios'
import QS from 'qs'
import { message } from 'ant-design-vue'

const DEFAULT_CONFIG = {
  BASE: '/api/',
  WITHCREDENTIALS: true,
  TIMEOUT: 30000
}

class ApiCreator {
  constructor (config) {
    // axios默认配置
    this.config = { ...DEFAULT_CONFIG, ...config }
    Axios.defaults.baseURL = this.config.BASE
    Axios.defaults.headers.post['Accept'] = 'application/json'
    Axios.defaults.headers.post['X-Requested-With'] = 'XMLHttpRequest'
    Axios.defaults.timeout = this.config.TIMEOUT
    Axios.defaults.withCredentials = this.config.WITHCREDENTIALS
    // 添加请求拦截器
    Axios.interceptors.request.use(config => {
      // 在发送请求之前做些什么
      return this.config.beforeRequest(config)
    }, error => {
      // 对请求错误做些什么
      this.config.requestError && this.config.requestError(error)
      return Promise.reject(error)
    })
    // 添加响应拦截器
    Axios.interceptors.response.use(function (response) {
      // 对响应数据做点什么
      if (response.data.code === 0) {
        return response.data.data
      } else {
        message.error(response.data.msg)
        return Promise.reject(response.data.msg)
      }
    }, function (error) {
      // 对响应错误做点什么
      this.config.responseError && this.config.responseError(error)
      return Promise.reject(error)
    })
    this.methods = this.__getMethods()
  }

  // 创建api
  create () {
    const modules = this.config.MODULES
    const apiModules = {}
    for (const module in modules) {
      const apiModule = {}
      modules[module].forEach((item) => {
        apiModule[item.name] = (params) => {
          item.params = params
          return this.excute(item)
        }
      })
      apiModules[module] = apiModule
    }
    return apiModules
  }

  // 方法聚合
  __getMethods () {
    const that = this
    return {

      // GET请求
      get (opts) {
        const params = opts.params || {}
        const options = {
          url: opts.url,
          method: 'get',
          responseType: opts.responseType || 'json',
          meta: opts.meta,
          params: params
        }
        return that.__request(options)
      },

      // POST请求:原理同get基本一样，但是要注意的是，post方法必须要使用对提交从参数对象进行序列化的操作，所以这里我们通过node的qs模块来序列化我们的参数。这个很重要，如果没有序列化操作，后台是拿不到你提交的数据的。这就是文章开头我们import QS from 'qs'的原因。
      post (opts) {
        const params = opts.params || {}
        const options = {
          url: opts.url,
          method: 'post',
          meta: opts.meta,
          data: QS.stringify(params)
        }
        return that.__request(options)
      },

      // 上传
      upload (opts) {
        const params = opts.params || {}
        const formData = new FormData()
        for (const k in params) {
          formData.append(k, params[k])
        }
        const options = {
          url: opts.url,
          method: 'post',
          meta: opts.meta,
          data: formData,
          headers: { 'Content-Type': 'multipart/form-data' }
        }
        return that.__request(options)
      },

      // PUT请求
      put (opts) {
        const params = opts.params || {}
        const options = {
          url: opts.url,
          method: 'put',
          meta: opts.meta,
          data: QS.stringify(params)
        }
        return that.__request(options)
      },

      // DELETE请求
      delete (opts) {
        const params = opts.params || {}
        const options = {
          url: opts.url,
          method: 'delete',
          meta: opts.meta,
          data: QS.stringify(params)
        }
        return that.__request(options)
      }
    }
  }

  /**
   * 执行请求
   * @param options 请求参数对象
   */
  excute (options) {
    // 方法验证
    if (this.methods[options.method] === undefined) {
      console.error('请求' + options.name + '的方法不正确！')
      return
    }
    // 如果没有相应权限
    const method = this.methods[options.method]
    // 返回可以cancel的axios实例
    return method(options)
  }

  /**
   * 执行请求
   * @param options 请求参数设置
   */
  __request (options) {
    options = { ...options }
    return Axios(options)
  }
}

export default ApiCreator

```

最后在main.js中

```javascript
// 引入api
import api from '@/api'
// api绑定到vue上
Vue.$api = Vue.prototype.$api = api
```



##### 注意：关于axios的封装的另一种方式：

```javascript
//响应拦截器
axios.interceptors.response.use(
    response=>{
    //如果返回的状态码为200，说明接口请求成功，可以拿到正常数据
    //否则的话抛出错误
    //200只代表接口正常调通了，但是业务逻辑处理后，也可能会有业务逻辑上的状态。这个就需要后端自己定义自己的返回结构了。例如上文axios的封装。
    if(response.getStatusCode()===200){
        return Promise.resolve(response)
    }else{
        return Promise.reject(response)
    }
},
    //服务器状态码不是2开头的情况
    //这里可以跟后台开发人员协商好统一的错误代码，然后根据返回的状态码进行一些操作，例如登陆过期，错误提示等等。具体的需求要具体分析。
    //下面列举几个常见的操作，其他需求可自行扩展。
    error=>{
        if(error.response.status){
            swith(error.response.status){
                //401:未登录
                case 401:一堆代码 break;
                //403:过期
                case 403:一堆代码 break;
                //404:请求不存在
                case 404:一堆代码 break;
                //其他错误
                default:一堆代码
            }
          return Promise.reject(error.response) 
        }
    }
})
```

##  
