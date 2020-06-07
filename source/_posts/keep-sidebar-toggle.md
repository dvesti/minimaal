---
title: Удерживаем Sidebar в окне
date: 2018-02-17 14:37:56
tags: [css, Next]
categories: News
---

#### Восстановим переключатель боковой панели

##### Шаг 01

Открываем в текстовом редакторе файл `/themes/next/source/css/_common/components/sidebar/sidebar.styl` и комментируем строчки `tablet` и `mobile`
```js
+tablet() {
    display: none !important;
}
+mobile() {
  display: none !important;
}
```
<!--more-->
##### Шаг 02

Открываем с помощью текстового редактора файл `/themes/next/source/css/_common/components/sidebar/sidebar-toggle.styl` и также комментируем строчки `tablet` и `mobile`
Вместо них добавляем эти строчки:
```css
+tablet() {
  right: 20px;
  bottom: 45px;  //Указываем точное место расположения
  -moz-opacity: 0.8;  
  -khtml-opacity: 0.8;  
  opacity: 0.8;  //Увеличиваем эффект прозрачности
  /*display: none;*/
}
+mobile() {
  right: 20px;
  bottom: 45px;  //Указываем точное место расположения
  -moz-opacity: 0.8;  
  -khtml-opacity: 0.8;  
  opacity: 0.8;  //Увеличиваем эффект прозрачности
  /*display: none;*/
}
```
Открываем в текстовом редакторе этот файл - `/themes/next/source/css/_common/components/back-to-top.styl` и также комментирием и меняем, как в предыдущем описании
```css
+mobile() {
  right: 20px;
  -moz-opacity: 0.8;  
  -khtml-opacity: 0.8;  
  opacity: 0.8;  
  /*display: none;*/
}
+tablet() {
  right: 20px;
  -moz-opacity: 0.8;  
  -khtml-opacity: 0.8;  
  opacity: 0.8;  
  /*display: none;*/
}
```

#### Изменяем боковую панель

Открываем `layout/_macro/sidebar.swig` и ищем `sidebar-dimmer`
Должен выглядеть так:
```html
<aside id="sidebar" class="sidebar">
  <div id="sidebar-dimmer"></div>
  <div class="sidebar-inner">
```
Прописываем стили для `sidebar-dimmer`в файле `source/css/_common/components/sidebar/sidebar-toggle.styl`

```css
.sidebar-active #sidebar-dimmer {
  opacity: .7;
  -webkit-transform: translateX(-150%);
  transform: translateX(-150%);
  transition: opacity .2s;
}

#sidebar-dimmer {
  display: none;
  position: absolute;
  top: 0;
  left: 100%;
  width: 200%;
  height: 100%;
  background: #000;
  opacity: 0;
  transition: opacity .2s,transform 0s .2s;
  +mobile() {
    display: block;
  }
}
```
И добавляем в файле `source/js/src/motion.js` следующее:

```js
var sidebarToggleMotion = {
  toggleEl: $('.sidebar-toggle'),
  dimmerEl: $('#sidebar-dimmer'),  //init
  sidebarEl: $('.sidebar'),
  isSidebarVisible: false,
  init: function () {
    this.toggleEl.on('click', this.clickHandler.bind(this));
    this.dimmerEl.on('click', this.clickHandler.bind(this));   //binding
    this.toggleEl.on('mouseenter', this.mouseEnterHandler.bind(this));
    this.toggleEl.on('mouseleave', this.mouseLeaveHandler.bind(this));
```
В последней версии - это уже указано.

[Источник](https://blog.zzbd.org/2017/06/10/keep-sidebar/)