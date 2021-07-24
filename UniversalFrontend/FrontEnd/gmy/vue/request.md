 

```
// 封装请求
import axios from "axios";
import store from "../store";
import * as Types from "../store/mutations-types";
import { Toast } from "cube-ui";

class Ajax {
  constructor() {
    // 定义一些公共参数
    this.baseURL =
      process.env.NODE_ENV === "production" ? "www.baidu.com" : "/";
    this.timeout = 5000;
    this.queue = {}; // 创建一个队列
  }
  setInterceptors(instance) {
    // 请求拦截
    instance.interceptors.request.use(
      config => {
        this.queue.url = config.url;
        // 如果队列的长度大于0 就显示正在加载
        if (Object.keys(this.queue).length > 0) {
          this.toast = Toast.$create({
            txt: "正在加载",
            time: 0
          });
          this.toast.show();
        }

        // 每次请求时候拿到一个终止请求的令牌 存到vuex中
        const Cancel = axios.CancelToken;
        config.CancelToken = new Cancel(c => {
          store.commit(Types.PUSH_TOKEN, c);
        });
        return config;
      },
      err => err
    );
    // 响应拦截
    instance.interceptors.response.use(
      res => {
        // 每次响应之后就从队列里面删除
        delete this.queue.url;
        if (Object.keys(this.queue).length === 0) {
          this.toast.hide();
        }
        return res.data;
      },
      err => {
        // 每次响应之后就从队列里面删除
        delete this.queue.url;
        if (Object.keys(this.queue).length === 0) {
          this.toast.hide();
        }
        Promise.reject(err);
      }
    );
  }
  request(options) {
    let instance = axios.create();
    // 设置拦截器
    this.setInterceptors(instance);
    // 合并一下用户传的参数和默认参数
    const config = {
      baseURL: this.baseURL,
      timeout: this.timeout,
      ...options
    };
    return instance(config);
  }
}
export default new Ajax();
```