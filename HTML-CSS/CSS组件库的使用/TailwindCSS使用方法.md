# TailwindCSS使用方法

1. 创建一个文件夹,我们会在里面放tailwindcss的所需要的东西

2. 先使用`npm init`,对package.json初始化

3. `npm install -D tailwindcss postcss-cli autoprefixer`

4. 用`code .`这个命令就能打开vscode

5. `npx tailwindcss init -p`,初始化tailwind.config.js文件和postcss.config.js文件

6. 在目录下建一个css文件,放入tailwind的三大核心部件

   ```css
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```

7. 在package.json文件中的scripts中加入以下两句话

   ```json
    "watch": "postcss css/style.css -o dist/style.css --watch",
       "build": "cross-env NODE_ENV=production postcss css/style.css -o dist/style.css "
   ```

   ==注意==在build下要加入cross-env这个插件,这样子打包缩减的时候才不会报错

   ```js
   npm install cross-env -D
   ```

   

   * watch:是用postcss将css目录下的style.css输出到dist目录下的style.css,--watch是用来监视的,在文件更新的时候会重复执行这个操作

     > npm run watch

   * build:是用来在生产环境中,对于没有用到的css样式进行去除,打包精简

     > npm run build

8. autoprefixer是用来自动添加浏览器的前缀的

9. 在tailwind.config.js下,purge这个下加上这样的一句话

   ```js
   './dist/**/*.html'
   ```

   这个是搭配上文中的build一起使用的,这句话就是该目录下的所有html文件,可以视情况而定

