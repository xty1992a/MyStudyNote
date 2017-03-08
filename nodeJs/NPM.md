#NPM

npm(Node Package Manager)是一个nodejs的包管理平台,随着node的兴起,js相关的库,模块等都可以通过这个平台进行共享;

npm与Node.js一起被安装,通过cmd命令行可以执行npm命令,前提是配置好环境变量;

npm命令

1. npm init 引导创建package.json文件
	主要关注name和version,其他enter即可
2. npm config 管理npm的配置路径
	基础语法:
	```
	npm config set <key> <value> [-g]
	npm config delete <key>
	npm config list
	npm config edit
	npm get <key>
	npm set <key> <value> [-g|--global]
	```
	- 设置代理
		`npm config set proxy=http://dev-proxy.oa.com:8080`
	- 设置镜像地址
		`npm config set registry https://registry.npm.taobao.org`
	- 查/改全局安装目录
		`npm config get prefix`及`npm config set prefix path`

3. npm install/uninstall 安装/卸载模块
	参数为模块名,不加@默认安装最新版,加@并指定版本则下载指定模块
	安装位置是当前cmd运行目录下的`node_module`
	加入参数`-g`或`-global`为全局安装,将会安装到全局安装目录
	加入参数`-S`或`--save`会将包信息加入`dependencies`依赖包列表
	加入参数`-D`或`--save-dev`会将包信息加入`devDependencies`开发工具列表
	加入参数`-E`或`--save-exact`指定`dependencies`中指定包的精确版本
	不加参数默认会根据package.json中的dependencies项的列表安装模块
		
	删除使用 `uninstall`,`remove`,`rm`,`un`,`unlink`,其他参数如上

4. npm run	使用npm运行package.json中script中的命令
	script中可以设置一些cmd命令,使用 npm run '属性名'调用
```
//package.json
"scripts": {
    "start": "node bin/app.js"
}
//cmd命令
npm run start
//会自动运行 node bin/app.js	start属性名可以省略run
```
	






