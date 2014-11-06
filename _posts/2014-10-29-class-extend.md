---
layout: post
title: "深度复制的功能Class"
tags:
    -JavaScript
categories:
    -JavaScript
---
该代码中的Class来自infoQ的文章
[JavaScript的实例化与继承：请停止使用new关键字](http://www.infoq.com/cnarticlesjavascript-instantiation-and-inheritance)
下面是修改后的代码，在create方法中增加了深度复制的功能。

	var clone = function(sObj) {
			if (typeof sObj !== object) {
				return sObj;
			}
			if(sObj == null){
				return null;
			}
			var s = {};
			if (sObj instanceof Array) {
				s = [];
			}
			for (var i in sObj) {
				s[i] = clone(sObj[i]);
			}
			return s;
		}
	function Class() {}
	Class.extend = function extend(props) {
		var prototype = new this();
		var _super = this.prototype;
		for (var name in props) {
			if (typeof props[name] == function && typeof _super[name] == function) {
				prototype[name] = (function(super_fn, fn) {
					return function() {
						var tmp = this.callSuper;
						this.callSuper = super_fn;
						var ret = fn.apply(this, arguments);
						this.callSuper = tmp;
						if (!this.callSuper) {
							delete this.callSuper;
						}
						return ret;
					}
				})(_super[name], props[name])
			} else {
				prototype[name] = props[name];
			}
		}

		function Class() {}
		Class.prototype = prototype;
		Class.prototype.constructor = Class;
		Class.extend = extend;
		Class.create = Class.prototype.create = function() {
			var instance = new this();
			instance = clone(prototype);
			if (instance.init) {
				instance.init.apply(instance, arguments);
			}
			return instance;
		}
		return Class;
	}