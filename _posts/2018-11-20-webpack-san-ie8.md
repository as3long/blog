---
layout: post
title: "webpack san兼容ie8配置"
tags:
    -JavaScript
    -webpack
    -san
categories:
    javascript
---

```json
{
  "name": "front-end",
  "version": "0.0.2",
  "scripts": {
    "dev": "cross-env NODE_ENV=development webpack --mode=development --config webpack.config.js -w",
    "dist": "cross-env NODE_ENV=production webpack --mode=production --progress --config webpack.config.js"
  },
  "devDependencies": {
    "@babel/core": "^7.0.0",
    "@babel/plugin-proposal-class-properties": "^7.0.0",
    "@babel/plugin-proposal-decorators": "^7.0.0",
    "@babel/plugin-proposal-do-expressions": "^7.0.0",
    "@babel/plugin-proposal-export-default-from": "^7.0.0",
    "@babel/plugin-proposal-export-namespace-from": "^7.0.0",
    "@babel/plugin-proposal-function-bind": "^7.0.0",
    "@babel/plugin-proposal-function-sent": "^7.0.0",
    "@babel/plugin-proposal-json-strings": "^7.0.0",
    "@babel/plugin-proposal-logical-assignment-operators": "^7.0.0",
    "@babel/plugin-proposal-nullish-coalescing-operator": "^7.0.0",
    "@babel/plugin-proposal-numeric-separator": "^7.0.0",
    "@babel/plugin-proposal-optional-chaining": "^7.0.0",
    "@babel/plugin-proposal-pipeline-operator": "^7.0.0",
    "@babel/plugin-proposal-throw-expressions": "^7.0.0",
    "@babel/plugin-syntax-dynamic-import": "^7.0.0",
    "@babel/plugin-syntax-import-meta": "^7.0.0",
    "@babel/plugin-transform-member-expression-literals": "^7.0.0",
    "@babel/plugin-transform-property-literals": "^7.0.0",
    "@babel/plugin-transform-runtime": "^7.0.0",
    "@babel/preset-env": "^7.0.0",
    "@up/file-upload": "^1.0.6",
    "autoprefixer": "^6.7.7",
    "babel-loader": "^8.0.2",
    "clean-webpack-plugin": "^0.1.16",
    "cross-env": "^5.1.6",
    "css-loader": "^0.28.11",
    "file-loader": "^1.1.11",
    "html-webpack-plugin": "^3.2.0",
    "mini-css-extract-plugin": "^0.4.0",
    "postcss-loader": "^2.1.5",
    "postcss-preset-env": "^5.1.0",
    "precss": "^3.1.2",
    "style-loader": "^0.17.0",
    "uglifyjs-webpack-plugin": "^2.0.1",
    "url-loader": "^0.5.8",
    "webpack": "^4.19.0",
    "webpack-bundle-analyzer": "^3.0.3",
    "webpack-cli": "^3.1.0"
  },
  "dependencies": {
    "@babel/runtime": "^7.0.0",
    "babel-polyfill": "^6.26.0",
    "san": "^3.6.13",
    "san-router": "^1.2.0",
    "san-store": "^1.1.0"
  }
}

```

index.tpl
```html
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="keywords" content="<%=htmlWebpackPlugin.options.extra.keywords%>">
    <meta name="description" content="<%=htmlWebpackPlugin.options.extra.description%>"/>
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no,minimal-ui">
    <meta name="format-detection" content="telephone=no,email=no"/>
    <title><%=htmlWebpackPlugin.options.title%></title>
    <!--[if lt IE 9]>
    <script src="https://lib.baomitu.com/es5-shim/4.5.12/es5-shim.min.js"></script>
    <script src="https://lib.baomitu.com/es5-shim/4.5.12/es5-sham.js"></script>
    <script src="https://lib.baomitu.com/json3/3.3.2/json3.min.js"></script>
    <script src="https://lib.baomitu.com/console-polyfill/0.3.0/index.js"></script>
    <![endif]-->
    <!--[if IE]>
    <script src="https://lib.baomitu.com/es6-promise/4.1.1/es6-promise.auto.min.js"></script>
    <script>
        window.isIE = true;
    </script>
    <![endif]-->
    <script src="https://lib.baomitu.com/jquery/1.12.4/jquery.min.js"></script>
</head>
<body>
    <%=htmlWebpackPlugin.options.extra.content%>
</body>
</html>

```

.babelrc.js
```js
const config = {
    presets: [
        [
            '@babel/preset-env',
            {
                targets: {
                    browsers: [
                        'ie >= 6',
                        '> 0.2%'
                    ]
                }
            }
        ]
    ],
    plugins: [
        '@babel/plugin-transform-property-literals',
        '@babel/plugin-transform-member-expression-literals',
        '@babel/plugin-transform-runtime',
        '@babel/plugin-syntax-dynamic-import',
        '@babel/plugin-syntax-import-meta',
        '@babel/plugin-proposal-class-properties',
        '@babel/plugin-proposal-json-strings',
        [
            '@babel/plugin-proposal-decorators',
            {
                legacy: true
            }
        ],
        '@babel/plugin-proposal-function-sent',
        '@babel/plugin-proposal-export-namespace-from',
        '@babel/plugin-proposal-numeric-separator',
        '@babel/plugin-proposal-throw-expressions',
        '@babel/plugin-proposal-export-default-from',
        '@babel/plugin-proposal-logical-assignment-operators',
        '@babel/plugin-proposal-optional-chaining',
        [
            '@babel/plugin-proposal-pipeline-operator',
            {
                proposal: 'minimal'
            }
        ],
        '@babel/plugin-proposal-nullish-coalescing-operator',
        '@babel/plugin-proposal-do-expressions',
        '@babel/plugin-proposal-function-bind'
    ]
};

module.exports = config;

```

postcss.config.js
```js
const config = {
    plugins: [
        require('precss'),
        require('autoprefixer')({
            browsers: ['last 3 versions', 'Android >= 4.0'],
        }),
    ]
};

// if (process.env.NODE_ENV !== 'development') {
//     config.plugins.push(require('postcss-sprites')({
//         spritePath: './images',
//         filterBy(image) {
//             // Allow only png files
//             if (!/__sprite/.test(image.url)) {
//                 return Promise.reject();
//             }

//             return Promise.resolve();
//         },
//         retina: true
//     }));
// }

module.exports = config;

```

webpack.config.js
```js
const path = require('path');
const webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');
// const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer');

const isDev = process.env.NODE_ENV === 'development';

const clientConfig = {
    // devtool: isDev ? '' : 'hidden-source-map',
    devtool: '',
    entry: {
        main: ['./js/main.js'],
    },
    resolve: {
        extensions: ['.js', '.vue', '.json'],
        alias: {
            san: isDev ? 'san/dist/san.dev.js' : 'san/dist/san.min.js'
        }
    },
    output: {
        path: isDev ? path.resolve(__dirname, '../public/report/ie/dev') : path.resolve(__dirname, '../public/report/ie/dist'),
        publicPath: isDev ? '/report/ie/dev/' : '//cdn.upchinaproduct.com/info/StockResearchReportWebServer/report/ie/dist/',
        filename: isDev ? '[name].js' : '[name].[chunkhash:8].js',
        chunkFilename: isDev ? '[name].js' : '[name].[chunkhash:8].js',
    },
    module: {
        rules: [{
            test: /\.js$/,
            exclude: /(node_modules)\\(?!@up)/,
            loader: 'babel-loader?cacheDirectory',
            options: {
                configFile: path.resolve(__dirname, './.babelrc.js')
            }
        }, {
            test: /\.css$/,
            exclude: /node_modules\\(?!@up)/,
            use: [
                MiniCssExtractPlugin.loader,
                isDev ? 'css-loader' : 'css-loader?modules=true&localIdentName=[local]&minimize=true'
            ]
        },
        {
            test: /\.scss$/,
            exclude: /node_modules/,
            use: [
                MiniCssExtractPlugin.loader,
                isDev ? 'css-loader' : 'css-loader?modules=true&localIdentName=[local]&minimize=true',
                'postcss-loader'
            ]
        },
        {
            test: /\.(png|jpg|jpeg|gif)$/,
            use: [{
                loader: 'url-loader',
                options: {
                    limit: 1,
                    name: isDev ? '[name].[ext]' : '[name]-[hash:8].[ext]'
                }
            }]
        }
        ]
    },
    plugins: [
        new webpack.DefinePlugin({
            'process.env': {
                NODE_ENV: `"${process.env.NODE_ENV}"`
            }
        }),
        new HtmlWebpackPlugin({
            title: '研报',
            inject: 'body',
            extra: {
                content: '<div id="app"></div>',
                description: '描述',
                keywords: '关键词'
            },
            filename: path.resolve(__dirname, '../views/indexIE.ejs'),
            chunks: ['manifest', 'vendor', 'main'],
            template: path.resolve(__dirname, './index.tpl')
        }),
        new MiniCssExtractPlugin({
            filename: isDev ? '[name].css' : '[name].[contenthash:8].css',
            // chunkFilename: isDev ? '[id].css' : '[id].[contenthash:8].css',
            allChunks: true
        }),
        // new BundleAnalyzerPlugin({ analyzerPort: 8919 })
    ],
    externals: {},
    optimization: {
        runtimeChunk: {
            name: 'manifest'
        },
        minimizer: [
            // 自定义js优化配置，将会覆盖默认配置
            new UglifyJsPlugin({
                exclude: /\.min\.js$/, // 过滤掉以".min.js"结尾的文件，我们认为这个后缀本身就是已经压缩好的代码，没必要进行二次压缩
                cache: true,
                parallel: true, // 开启并行压缩，充分利用cpu
                sourceMap: false,
                extractComments: false, // 移除注释
                uglifyOptions: {
                    compress: {
                        properties: false,
                        warnings: false
                    },
                    output: {
                        beautify: true,
                        quote_keys: true
                    },
                    mangle: {
                        ie8: true
                    },
                    sourceMap: false
                }
            })
        ],
        minimize: !isDev,
        splitChunks: {
            cacheGroups: {
                default: {
                    minChunks: 2,
                    priority: -20,
                }
            }
        }
    }
};

// 发布特殊逻辑
if (!isDev) {
    clientConfig.plugins.push(new CleanWebpackPlugin(
        ['dev', 'dist'], // 匹配删除的文件
        {
            root: path.resolve(__dirname, '../public/report/ie/'), // 根目录
            verbose: true, // 开启在控制台输出信息
            dry: false // 启用删除文件
        }
    ));
}

module.exports = clientConfig;

```

onhashchangePolyfill.js
```js
const onhashchangeArr = [];
const hashchange = 'hashchange';
const DOC = document;
const documentMode = DOC.documentMode;
const supportHashChange = (`on${hashchange}` in window) && (documentMode === undefined || documentMode > 7);

if (!supportHashChange) {
    const oldAttachEvent = window.attachEvent;
    window.attachEvent = function attachEvent(type, handler) {
        if (type === 'onhashchange') {
            onhashchangeArr.push(handler);
            // console.log('注册了事件', onhashchangeArr.length);
        }
        oldAttachEvent(type, handler);
    };
}

function onhashchangePolyfill() {
    if (supportHashChange) { return; }

    const location = window.location;
    let oldURL = location.href;
    let oldHash = location.hash;


    // check the location hash on a 100ms interval
    setInterval(() => {
        const newURL = location.href;
        const newHash = location.hash;

        // if the hash has changed and a handler has been bound...
        if (newHash !== oldHash) {
            // console.log('路由发生了变化');
            // execute the handler
            if (typeof window.onhashchange === 'function') {
                window.onhashchange({
                    type: 'hashchange',
                    oldURL,
                    newURL
                });
            }

            for (let i = 0, len = onhashchangeArr.length; i < len; i += 1) {
                const o = onhashchangeArr[i];
                o();
            }

            oldURL = newURL;
            oldHash = newHash;
        }
    }, 100);
}
onhashchangePolyfill();

```

event.js
```js
function stopEvent(event) {
    const e = event;
    if (window.event) { // 这是IE浏览器
        e.cancelBubble = true;// 阻止冒泡事件
        e.returnValue = false;// 阻止默认事件
    } else if (e && e.stopPropagation) { // 这是其他浏览器
        e.stopPropagation();// 阻止冒泡事件
        e.preventDefault();// 阻止默认事件
    }
}

function addEvent(el, type, fn) {
    if (document.addEventListener) {
        el.addEventListener(type, fn, false);
    } else {
        el.attachEvent(`on${type}`, function eventHandler(e) {
            e.target = e.target || e.srcElement;
            fn.call(this, e);
        });
    }
}

module.exports = {
    stopEvent,
    addEvent
};

```

storage.js
```js
/* eslint-disable */
/*!
 * 本地化存储(localStorage) 组件
 *
 * 版权所有(C) 2013 马超 (zjcn5205@yeah.net)
 *
 * 这一程序是自由软件，你可以遵照自由软件基金会出版的GNU通用公共许可证条款来修改和重新发布
 * 这一程序。或者用许可证的第二版，或者（根据你的选择）用任何更新的版本。
 * 发布这一程序的目的是希望它有用，但没有任何担保。甚至没有适合特定目的的隐含的担保。更详细
 * 的情况请参阅GNU通用公共许可证。
 * 你应该已经和程序一起收到一份GNU通用公共许可证的副本。如果还没有，写信给：
 * The Free Software Foundation, Inc., 675 Mass Ave, Cambridge, MA02139, USA
 */
/*
 *[功能描述]
 * 给不支持本地存储的浏览器创建一个 window.localStorage 对象来提供类似接口
 * 该对象支持以下方法或属性
	setItem : function(key, value)
	getItem : function(key)
	removeItem : function(key)
	clear : function()
	length : int
	key : function(i)
	isVirtualObject : true
 * 二次包装的接口 window.LS 提供以下方法和属性（如果有jQuery则同样会扩展该对象），推荐使用
	set : function(key, vlaue)
	get : function(key)
	remove : function(key)
	clear : function()
	each : function(callback) callback接受两个参数 key 和 value
	obj : function() 返回一个对象描述的localStorage副本
	length : int
 *
 *[已知问题、使用限制]
 * 原生本地存储的key是区分大小写的，模拟对象不区分（因为userData不区分key的大小写）
 * 模拟对象的 clear 方法仅仅能清理通过本组件设定的数据
 * 模拟对象的实际的存储容量跟原生本地存储有差异
 * 模拟对象不支持任何localStorage事件件
 *
 *[更新日志]
 * 2012-06-20 马超 创建
 * 2012-06-27 马超 增加clear相关方法和属性
 * 2012-07-02 马超 修改节点存储方式
 * 2012-07-03 马超 增加二次包装以优化接口使用
 * 2012-07-04 马超 修改内部逻辑，取消原有的单独存储key的方案，修改查询不存在key的时候的默认值为undefined
 * 2012-07-05 马超 增加二次包装的obj方法
 * 2013-03-06 胡志明 基于瑞星的刘瑞明提供的方案，兼容360急速浏览器IE模式（IE6），降低浏览器自带localStorage优先级，优先使用userData。
 * 2013-03-11 胡志明 恢复iframe代理创建head标签用户存储数据，修正了userData无法垮目录读写问题
 * 2013-03-14 胡志明 对部分无法创建iframe代理的浏览器尝试使用自带localStorage，如果不自带则暂时不支持本地存储
 * 2013-03-18 马超 优化加载判断逻辑和代码，以最大限度保证组件可用
 * 2013-04-23 马超 增加更多的错误处理，进一步提高浏览器的兼容性
 * 2013-05-04 马超 增加对userData的key的无效字符的转义处理功能
 * 2013-06-06 马超 优先探测本地存储，解决IE9下userData使用问题（刷新页面后无效）
 */
(function(window){
	//准备模拟对象、空函数等
	var LS, noop = function(){}, document = window.document, notSupport = {set:noop,get:noop,remove:noop,clear:noop,each:noop,obj:noop,length:0};

	//优先探测userData是否支持，如果支持，则直接使用userData，而不使用localStorage
	//以防止IE浏览器关闭localStorage功能或提高安全级别(*_* 万恶的IE)
	//万恶的IE9(9.0.11）)，使用userData也会出现类似seesion一样的效果，刷新页面后设置的东西就没有了...
	//只好优先探测本地存储，不能用再尝试使用userData
	(function(){
		// 先探测本地存储 2013-06-06 马超
		// 尝试访问本地存储，如果访问被拒绝，则继续尝试用userData，注： "localStorage" in window 却不会返回权限错误
		// 防止IE10早期版本安全设置有问题导致的脚本访问权限错误
		if( "localStorage" in window ){
			try{
				LS = window.localStorage;
				return;
			}catch(e){
				//如果报错，说明浏览器已经关闭了本地存储或者提高了安全级别
				//则尝试使用userData
			}
		}

		//继续探测userData
		var o = document.getElementsByTagName("head")[0], hostKey = window.location.hostname || "localStorage", d = new Date(), doc, agent;

		//typeof o.addBehavior 在IE6下是object，在IE10下是function，因此这里直接用!判断
		//如果不支持userData则跳出使用原生localStorage，如果原生localStorage报错，则放弃本地存储
		if(!o.addBehavior){
			try{
				LS = window.localStorage;
			}catch(e){
				LS = null;
			}
			return;
		}

		try{ //尝试创建iframe代理，以解决跨目录存储的问题
			agent = new ActiveXObject('htmlfile');
			agent.open();
			agent.write('<s' + 'cript>document.w=window;</s' + 'cript><iframe src="/favicon.ico"></iframe>');
			agent.close();
			doc = agent.w.frames[0].document;
			//这里通过代理document创建head，可以使存储数据垮文件夹访问
			o = doc.createElement('head');
			doc.appendChild(o);
		}catch(e){
			//不处理跨路径问题，直接使用当前页面元素处理
			//不能跨路径存储，也能满足多数的本地存储需求
			//2013-03-15 马超
			o = document.getElementsByTagName("head")[0];
		}

		//初始化userData
		try{
			d.setDate(d.getDate() + 36500);
			o.addBehavior("#default#userData");
			o.expires = d.toUTCString();
			o.load(hostKey);
			o.save(hostKey);
		}catch(e){
			//防止部分外壳浏览器的bug出现导致后续js无法运行
			//如果有错，放弃本地存储
			//2013-04-23 马超 增加
			return;
		}
		//开始处理userData
		//以下代码感谢瑞星的刘瑞明友情支持，做了大量的兼容测试和修改
		//并处理了userData设置的key不能以数字开头的问题
		var root, attrs;
		try{
			root = o.XMLDocument.documentElement;
			attrs = root.attributes;
		}catch(e){
			//防止部分外壳浏览器的bug出现导致后续js无法运行
			//如果有错，放弃本地存储
			//2013-04-23 马超 增加
			return;
		}
		var prefix = "p__hack_", spfix = "m-_-c",
			reg1 = new RegExp("^"+prefix),
			reg2 = new RegExp(spfix,"g"),
			encode = function(key){ return encodeURIComponent(prefix + key).replace(/%/g, spfix); },
			decode = function(key){ return decodeURIComponent(key.replace(reg2, "%")).replace(reg1,""); };
		//创建模拟对象
		LS= {
			length: attrs.length,
			isVirtualObject: true,
			getItem: function(key){
				//IE9中 通过o.getAttribute(name);取不到值，所以才用了下面比较复杂的方法。
				return (attrs.getNamedItem( encode(key) ) || {nodeValue: null}).nodeValue||root.getAttribute(encode(key));
			},
			setItem: function(key, value){
				//IE9中无法通过 o.setAttribute(name, value); 设置#userData值，而用下面的方法却可以。
				try{
					root.setAttribute( encode(key), value);
					o.save(hostKey);
					this.length = attrs.length;
				}catch(e){//这里IE9经常报没权限错误,但是不影响数据存储
				}
			},
			removeItem: function(key){
				//IE9中无法通过 o.removeAttribute(name); 删除#userData值，而用下面的方法却可以。
				try{
					root.removeAttribute( encode(key) );
					o.save(hostKey);
					this.length = attrs.length;
				}catch(e){//这里IE9经常报没权限错误,但是不影响数据存储
				}
			},
			clear: function(){
				while(attrs.length){
					this.removeItem( attrs[0].nodeName );
				}
				this.length = 0;
			},
			key: function(i){
				return attrs[i] ? decode(attrs[i].nodeName) : undefined;
			}
		};
		//提供模拟的"localStorage"接口
		if( !("localStorage" in window) )
			window.localStorage = LS;
	})();

	//二次包装接口
	window.LS = !LS ? notSupport : {
		set : function(key, value){
			//fixed iPhone/iPad 'QUOTA_EXCEEDED_ERR' bug
			if( this.get(key) !== undefined ) {
                this.remove(key);
            }
			LS.setItem(key, value);
			this.length = LS.length;
		},
		//查询不存在的key时，有的浏览器返回null，这里统一返回undefined
		get : function(key){
			var v = LS.getItem(key);
			return v === null ? undefined : v;
		},
		remove : function(key){ LS.removeItem(key);this.length = LS.length; },
		clear : function(){ LS.clear();this.length = 0; },
		//本地存储数据遍历，callback接受两个参数 key 和 value，如果返回false则终止遍历
		each : function(callback){
			var list = this.obj(), fn = callback || function(){}, key;
			for(key in list)
				if( fn.call(this, key, this.get(key)) === false )
					break;
		},
		//返回一个对象描述的localStorage副本
		obj : function(){
			var list={}, i=0, n, key;
			if( LS.isVirtualObject ){
				list = LS.key(-1);
			}else{
				n = LS.length;
				for(; i<n; i++){
					key = LS.key(i);
					list[key] = this.get(key);
				}
			}
			return list;
		},
		length : LS.length
	};
	//如果有jQuery，则同样扩展到jQuery
	if( window.jQuery ) window.jQuery.LS = window.LS;
})(window);

module.exports = LS;

```