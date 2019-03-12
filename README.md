# kfc-frame

## 功能
提供外层导航结构，包含头导航栏、左侧导航栏及主显示区域。

- 头导航栏拆分为左侧logo区域、中央导航区域及右侧用户区域。三个区域都可定制化自己的组件，并将其插入相应的位置（也可使用已经提供的组件，也可不填冲，使其不显示）。
- 右侧导航栏、主显示区域也可以进行定制。支持只有主显示区域和包含两块区域的场景。
- 支持头导航栏与左侧导航栏之间的联动。

## 维护者
k2liumc

## 依赖
无

## kfc-frame属性
| 属性                    | 说明                           | 类型                 | 默认值        |
| ----------------------- | ------------------------------ | -------------------- | ------------- |
| headerMenu|头导航栏结构。| Array|[]|
| siderMenuMap|左侧导航栏map，key为头导航栏item的name值，值为右侧显示的导航栏结构。此处siderMenu失效。| Object |{}|
| siderMenu|在没有头导航栏页面中，此处为左侧导航栏结构。|Array|[]|

## kfc-sider、kfc-header-menu属性
| 属性        | 说明     | 类型   | 默认值 |
| ----------- | -------- | ------ | ------ |
|title|显示的菜单名称。|String|''|
|name|对应的路由name。|String|''|
|icon|左侧显示的图标。|String|''|
|children|子菜单,头导航栏暂时没有。|Array|[]

## 示例
1、在router文件中引入并配置在根节点中，许下：
```bash
import KFCFrame from '@/components/kfc-frame'

  routes: [
    {
      path: '/',
      name: 'index',
      component: KFCFrame,
```
2、在src目录下创建menu文件夹，在menu文件夹下创建menu.js文件，文件格式如下:
```bash
1)只有头导航栏菜单，无左侧导航栏
module.exports = {
  headerMenu: [
    {
      name: 'dataset.list',
      icon: 'md-person',
      title: '数据管理'
    },
    {
      name: 'model.list',
      icon: 'md-person',
      title: '模型管理'
    }
  ]
}
```
```bash
2)有左侧导航栏，无头导航栏
module.exports = {
  siderMenu: [
    {
      name: 'dataset.list',
      icon: 'md-person',
      title: '数据管理'
    },
    {
      name: 'model.list',
      icon: 'md-person',
      title: '模型管理',
      children: [
        {
          name: 'model.add',
          icon: 'md-person',
          title: '模型录入'
        },
        {
          name: 'model.query',
          icon: 'md-person',
          title: '模型查询'
        }
      ]
    }
  ]
}
```
```bash
3)既有头导航栏，也有左侧导航栏
module.exports = {
  headerMenu: [
    {
      name: 'dataset',
      icon: 'md-person',
      title: '数据管理'
    },
    {
      name: 'model',
      icon: 'md-person',
      title: '模型管理'
    }
  ],
  siderMenuMap: {
    'dataset': [
      {
        name: 'dataset.add',
        icon: 'md-person',
        title: '数据录入'
      },
      {
        name: 'dataset.query',
        icon: 'md-person',
        title: '数据查询'
      }
    ],
    'model': [
      {
        name: 'model.add',
        icon: 'md-person',
        title: '模型录入'
      },
      {
        name: 'model.query',
        icon: 'md-person',
        title: '模型查询'
      }
    ]
  }
}
```
