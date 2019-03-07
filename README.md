# kfc-frame

## 功能
提供外层结构，包含头导航栏、左侧导航栏及主显示区域。
1.头导航栏拆分为左侧logo区域、中央导航区域及右侧用户区域。三个区域都可定制化自己的组件，并将其插入相应的位置（也可使用已经提供的组件，也可不填冲，使其不显示）。
2.右侧导航栏、主显示区域也可以进行定制。支持只有主显示区域和包含两块区域的场景。
3.支持头导航栏与左侧导航栏之间的联动。

## 维护者
k2liumc

## 依赖
无

## kfc-frame属性

| 属性                    | 说明                           | 类型                 | 默认值        |
| ----------------------- | ------------------------------ | -------------------- | ------------- |
| headerMenu|头导航栏结构。| Array|[]|
| siderMenuMap|左侧导航栏map，key为头导航栏item的name值，值为右侧显示的导航栏结构。此处siderMenu失效。| Object |{}|
| siderMenu|在没有头导航栏页面中，此处为左侧导航栏结构。|Func(selectedFields)|Array|[]|

## kfc-sider、kfc-header-menu属性
| 属性        | 说明     | 类型   | 默认值 |
| ----------- | -------- | ------ | ------ |
|title|显示的菜单名称。|String|''|
|name|对应的路由name。|String|''|
|icon|左侧显示的图标。|String|''|
|children|子菜单,头导航栏暂时没有Array。|null|

## 示例
```
router文件的index
```bash
import KFCFrame from '@/components/kfc-frame'

  routes: [
    {
      path: '/',
      name: 'index',
      component: KFCFrame,
```
```
修改kfc-frame.vue，将导航栏结构传过去。
```
