# DengPu 登扑 Vue实战项目

# 在这个APP中实现（目标）
1. 哈登新闻、图片及视频的获取与展示
   1. 不同大小卡片镶嵌式列表展示
   2. 点赞及消息提示的防抖功能
2. 比赛及数据的可视化显示
3. 登录注册功能

*暂时用手动设置后的EasyMock上的端口来代替真实的数据*
  
  地址：https://www.easy-mock.com/project/5d4f6b52bfbd2538192571c7

## 使用到的插件记录或库
1. vue-awesome-swiper
2. better-scroll
3. JSONPlaceholder
4. Vant
5. ElementUI
6. EasyMock 

## 记录 
1. 完成footer的制作和跳转 完成首页的基本布局 制作item组件
2. 通过Easy Mock网站提供自定义的接口 
3. 完成社区页面中的标签页组件的制作,sticky定位,实现增删兴趣项的功能，并使用localStorage实现了状态的存储
4. 修改首页布局，用不对称的卡片式列表展示新闻动态，实现点赞按钮的防抖

## 开发中遇到的问题及思考

### 字体图标通过v-for遍历展示时，使用模板数据展示无效
+ 给元素加上v-html属性，进行转义显示
### 路由高亮的方式 路由重定向后高亮丢失的问题
+ 高亮的两种方式
   1. router自带的router-link-active类，在上面增加样式(注意router-link-exact-active是精确匹配,会导致路由高亮丢失)
   2. 给属性linkActiveClass赋值自定义的样式MyActive
### 过渡与动画效果 只能依赖于元素的插入、更新或销毁吗
### 在localStorage中的数据存入与读取
1. 注意需要通过JSON.stringify转化成字符串来存储
2. 读取时如果数据与计算属性绑定，会报错，因此需要给读出的数据一个默认值（通过||默认值的方式）
### 使用position:sticky时安卓设备的兼容存在问题 慎用！
### 在开发时注意按需加载插件 异步加载组件
1. 同级的组件在引入的时候需要需要增加地址前缀，否则回去node_modules中寻找而报错
### 两行式卡片展示 如果直接使用flex布局或者组件库中给出的栅格布局，不能直接实现卡片嵌入的效果
1. 解决方式：将单列ul变为两列ul，可以实现卡片嵌入的效果，但是也带来了额外的开销
### 在为图片点赞时避免频繁点击，需增加防抖
1. 采用从工具类utils文件夹中导入helper.js中自定义的Debounce方法(按需加载)
2. 根据点赞功能的基本需求，设置为先进行一次点赞再防抖
3. 注意防抖函数中的this指向问题，因为Debounce方法的返回值是函数
### 白屏时间2s 需优化
1. 引入骨架图 vant框架中的不好用（原因未知） 
2. 手动实现简易的骨架图，能先出现骨架图再出现组件，但并没有性能提升