## 跨域读写Cookie
+ 利用html script 标签跨域写Cookie。但由于有些浏览器开启了隐私保护策略，即使往不同域下写入了cookie，也不一定能读取出来 ，所以就有了W3C制定的P3P协议。
+ P3P协议， 通过在response的头中加入P3P协议，就可以使往跨域写cookie成功。
+ 通过URL参数实现跨域信息传递。 如果通过上面两种还不能满足条件，则可以采用此方法。但此方法只能同时传递给一个域。

## 跨域frame通信
1. 相同跨下的frame可以相互访问。
    + 父级想访问子frame中的元素，通过$(id)[0].contentWindow 即可得到子frame对象
    + 子frame想访问父级，可通过***window.parent*** 。如果是多级frame嵌套，frame想要访问最顶级父级，可通过***window.top*** 得到顶级父元素对象。
2. 相同父级跨，但不同子级跨下的访问时，需要同时把相互访问的页面的域提升到顶级域即可相互访问。使用: ***document.domain="###.###"***
3. 不同域之间的通信，有两个方式可以实现。
    + 使用中间页面传参数，即在frame中先通过跳转至与目标页面同域下的一中间页面，并且带上参数，然后再通过中间页面与目标页面进行参数的传递。
    + 使用HTML5中的postMessage API接口来实现相互通信。实现代码如下： 
    ```javascript
    /**
     * 封装postMessage方法，使发出的信息能被通用的message listener处理
     * @param {Window} targetWindow 目标框架窗口
     * @param {String} cmd  在目标窗口window空间中存在的方法名，消息发送后，目标窗口执行此名称的方法
     * @param {Array} args cmd方法需要的参数，多个参数时使用数组
     * @param {Function} callback 可选的参数，如果希望获得目标窗口的执行结果，使用此参数，结果返回后自动以返回结果为参数调用此回调方法
     */
    function sendFrmMsg(targetWindow, cmd, args, callback) {
        var fname;
        if (callback) {
            fname = "uuid" + new Date().getTime(); //生成唯一编码 
            window[fname] = callback;
        }

        args = (args instanceof Array) ? args : [args];

        var msg = {
            cmd: cmd, // "setVal"
            args: args, // [document.title]
            returnCmd: fname // option
        }

        targetWindow.postMessage(JSON.stringify(msg), "*");
    }

    /**
     * 获取另一个跨域窗口上的变量值
     * @param {Window} targetWindow 目标框架窗口
     * @param {String} varName 待获取值的变量名称
     * @param {Function} callback 获取成功后调用此回调方法处理变量值
     */
    function getFrmVarValue(targetWindow, varName, callback) {
        sendFrmMsg(targetWindow, "getOtherFrameVarValue", [varName], callback);
    }

    /**
     * 给另一窗口设置变量值
     * @param {Window} targetWindow 目标框架窗口
     * @param {String} varName 待设置变量名
     * @param {Object} value 待设置变量值
     */
    function setFrmVarValue(targetWindow, varName, value) {
        sendFrmMsg(targetWindow, "setOtherFrameVarValue", [varName, value]);
    }

    /**
     * 获取窗口变量值
     * @param {String} varName 变量名称
     */
    function getOtherFrameVarValue(varName) {
        try {
            eval("var ret = " + varName);
            return ret;
        } catch (e) {
            console.log(e);
        }
    }

    /**
     * 设置变量值
     * @param {String} varName 变量名称
     * @param {Object} value 变量值
     */
    function setOtherFrameVarValue(varName, value) {
        try {
            if (typeof value === "string") { // 字符串类型在拼接表达式时需要加引号
                value = "'" + value + "'";
            }
            eval(varName + "=" + value);
        } catch (e) {
            console.log(e);
        }
    }

    /**
     * message 事件监听器，自动根据cmd执行
     * @param {Object} evt
     * obj 形式  
     * ｛
     * 		cmd: "目标窗口的function引用名",
     *         args: "参数列表" , 数组形式,
     *         [returnCmd]: "可选的，表示双向调用的回调function引用名，在回调时"
     *	    ｝
    */
    window.onmessage = function(evt) {
        evt = evt || event;

        var source = evt.origin;

        try {
            var obj = JSON.parse(evt.data);
            console.log(obj);
        } catch (e) {
            console.log(e);
        }
        
        if (obj.cmd) { obj["arg0"] = "title"
    // setVal(obj.arg0, obj.arg1, obj.args);
            var cmd = obj.cmd + "(";

            if (obj.args) {

                for (var i = 0; i < obj.args.length; ++i) {
                    obj["arg" + i] = obj.args[i];
                    if (i > 0) {
                        cmd += ",";
                    }
                    cmd += "obj.arg" + i;
                }
            }

            cmd += ")";
            // 以上代码完成后，如obj.cmd="fun"，则拼接字符串如下：fun(obj.arg1, obj.arg2);
            // 在通过eval执行时，各参数即obj.arg1等已绑定到obj对象上，所以取的是传递过来的参数数组值
            try {
                var ret = eval(cmd);
                if (obj.returnCmd) {
                    evt.source.postMessage(JSON.stringify({
                        cmd: obj.returnCmd,
                        args: [ret]
                    }), evt.origin);
                }
            } catch (e) {
                if (console) console.log(e);
            }
        }
    }
    ```