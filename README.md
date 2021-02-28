
#### 运行

> 项目后端服务器是基于node、MySQL开发，运行前请确认系统已安装相关应用 

##### 服务器端

+ 确认是否全局安装`nodemon`

+ 若无安装：

  + `npm i -g nodemon`

  + 或修改`web-server/package.json`

    ```javascript
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "dev": "set PORT=3000 && node main.js",
        "build": "babel src -d dist",
        "start": "node dist/app.js"
      },
    ```

+ `cd web-server`
+ `mkdir -p public/uploads`  新建uploads文件夹保存商品图片
+ 将`web-server`文件夹下的`webshop.sql`导入`MySQL`数据库中
+ `npm install` 安装依赖
+ 修改`web-server/src/config.js`文件，此文件记录项目的全局变量，在文件中找到`password`、`database`、`user`属性，根据你的数据库信息修改它们的值
+ `npm run dev` 在本地运行，启动服务器

##### 客户端

- `cd web-client`
- `mkdir static` 新建static文件夹，防止报错
- `npm install` 安装依赖
- `npm run dev` 在本地运行
- 接着就可以在`http://localhost:8080`下访问到该项目
