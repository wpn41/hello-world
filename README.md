# hello-world
just another respository
1. webpack概念
	1) webpack是什么？
		webpack是一个模块化的打包工具。
		
	2) webpack有什么用？
		可以把网页上用到的所有资源都进行打包，包含： JS模块（CommonJS、CMD、AMD、ES6）、CSS、LESS、图片、音频...
		生成一个最终的.js文件，所有资源都变成了文字代码模块，在页面上可以直接使用
		
2. webpack安装使用【重点】
	1) 全局安装
		cnpm i -g webpack@1.14.0
		
	2) 本地安装
		cnpm i webpack@1.14.0 --save-dev
		
	3) 编写模块化代码
		a.js
		b.js
		
	4) 打包
		webpack 入口文件  出口文件
		webpack ./js/a.js ./bundle.js
		
	5) 使用打包后的文件
		编写.html文件，引入 bundle.js
		
3. 编写配置文件【重点】
	在项目根目录下创建文件名： webpack.config.js
	
	配置文件的写法：
		//1) 引入webpack模块
		var webpack=require('webpack');
			
		//2) 暴露配置信息
		module.exports={
			//3) 入口文件声明
			entry:'./js/a.js',
			
			//4) 出口文件声明
			output:{
				//声明生成文件的路径
				path:'./output/',
				//声明生成文件的文件名
				filename:'bundle.js',
				//公共的静态文件路径
				publicPath:'output/'
			}
		}

4. 配置加载器【重点】（webpack默认只支持JS模块，如果要打包其它模块必须安装加载器支持）
	1) 前提条件：如果要使用加载器，必须先安装再使用
	2) 安装加载器
		cnpm i css-loader style-loader --save-dev
		
	3) 配置加载器
		module.exports={
			...
			module:{
				loaders:[
					//第一条都是一个加载器
					//加载器的语法： {test:/.../, loader:'***-loader!***-loader'}
					//CSS加载器
					{test:/\.css$/, loader:'style-loader!css-loader'}
				]
			}
		}

5. 其它
	1) webpack-dev-server开发打包服务器
		a. 安装
			全局安装： cnpm i -g webpack-dev-server@1.16.2
			本地安装： cnpm i webpack-dev-server@1.16.2 --save-dev
			
		b. 使用
			webpack-dev-server //运行开发打包服务器，所有更改自动打包
			webpack-dev-server --hot --inline //热部署、热刷新
			
	2) 多入口
		entry:{
			文件名:'要打包的文件路径',
			文件名:'要打包的文件路径'
		}
		//多出口
		output:{
			filename:'[name].js'//文件名类型
		}

	3) 插件
		module.exports = {
			.................
			plugins:[
				//注释添加到生成的文件的头部
				new webpack.BannerPlugin("webpack 打包制作"),
				// 提供公共代码
				// 默认会把所有入口节点(index和c)的公共代码提取出来,生成一个common.js
		 		new webpack.optimize.CommonsChunkPlugin('common.js')
			]
		}
