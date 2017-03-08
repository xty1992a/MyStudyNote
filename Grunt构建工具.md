#Grunt构建工具

Grunt是一个依托npm平台的项目构建工具,依靠它的插件系统形成了一个强大的生态圈

###安装grunt
1. 全局安装grunt-cli(命令行工具)
	`npm install grunt-cli -g`
2. 在项目内安装grunt
	`npm install grunt --save-dev`
3. 创建`Gruntfile.js`grunt配置js文件
	该文件实际上是一个模块,模块内主要分三部分:
	- 插件配置`grunt.initConfig({})`
		配置对象的每一个属性对应一个插件,插件内可以视情况进行默认配置
		每个插件可以设置多个任务,任务设置视插件而定
	- 加载插件`grunt.loadNpmTasks('grunt-contrib-concat')`
		一个loadNpmTasks()调用一个插件,参数为插件名,插件名将会作为配置对象的属性名
	- 注册任务`grunt.registerTask('default', ['concat'])`
		注册名为`grunt value`命令的值,设置为default可以省略value
		任务名写在第二个参数数组中
		`第一个参数建议放代码检查,watch必须写在最后`

	代码示例:
```
module.exports = function(grunt){
// 1. 初始化插件配置
    grunt.initConfig({
        //主要编码处
        concat:{
            options: { //可选项配置
                separator: ';'   //使用;连接合并
            },
            dist:{
                src: ['src/js/*.js'],
                dest: 'build/js/built.js'
            }
        }

    });
// 2. 加载插件任务
    grunt.loadNpmTasks('grunt-contrib-concat');
// 3. 注册构建任务
    grunt.registerTask('default', ['concat']);
};
```

	*特殊插件*
	- 语法检查插件(jshint)
		该插件须配合`.jshintrc`配置文件使用,指定语法检查相关项;该插件在Gruntfile中的设置如下:
	```
	jshint : {
            options: {
                jshintrc : '.jshintrc' //指定配置文件
            },
            build : ['Gruntfile.js', 'src/js/*.js'] //指定检查的文件
        }
	```
	- 自动编译插件(watch)
		该插件必须在插件列表的最后,执行到它时,程序会挂起,后面的插件无法得到执行;
	```
        watch : {
            scripts : {
                files : ['src/js/*.js', 'src/css/*.css'],
                tasks : ['concat', 'jshint', 'uglify'],// , 'cssmin'],
                options : {spawn : false}
            }
        }
	```
		