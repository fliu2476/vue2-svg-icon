# vue2-svg-icon  
> 本项目是在cenkai88的[vue-svg-icon](https://github.com/cenkai88/vue-svg-icon)项目上修改的，移除了一些我不需要的功能，props也做了一些修改。请移步[vue-svg-icon](https://github.com/cenkai88/vue-svg-icon)

##### v1.3.2


## Usage
### 1. install
```
npm install vue2-svg-icon --save-dev
```
### 2. put your svg into src/assets/svg/
- **this dir are not supported to be configured now**  
- **src folder should be in the same folder with node_modules**

### 3. import vue2-svg-icon in your main.js
```
import Icon from 'vue2-svg-icon/Icon.vue';
Vue.component('icon', Icon);  
```
### 4. use the svg icon in your vue!
- name: svg file name
- w: width (accept String or Number)
- h: height (accept String or Nnmber)
```
<icon name="chameleon" :w="24" :h="24"></icon>
```

### Trouble Shooting
1. cannot find corresponding .svg file in vue2-svg-icon/svg when you inject it in main.js, please keep the name in main.js and the filename exactly same.
```
[Vue warn]: Invalid prop: custom validator check failed for prop "name". 
```
2. cannot find the "svg" fold in src folder
```
This dependency was not found:
   
   * !xml-loader!../../src/svg in ./~/.6.4.1@babel-loader/lib!./~/.11.1.4@vue-loader/lib/selector.js?type=script&index=0!./~/.1.2.8@vue2-svg-icon/Icon.vue
   
   To install it, you can run: npm install --save !xml-loader!../../src/svg
```
3. pls check the .babelrc file of root folder
```
Module build failed: ReferenceError: Unknown plugin "transform-runtime"
 specified in "/Users/test/Desktop/Dev/github/.babelrc" at 0, attempted to resolve relative to 
 "/Users/test/Desktop/Dev/github"
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
