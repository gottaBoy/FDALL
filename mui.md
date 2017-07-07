## mui中拨打电话有两种方式：

## 第一种：直接调用mui封装方法，这种方法相对比较简单

        document.getElementById("telephone").addEventListener('tap',function(){
            var btnArray=['拨打','取消'];
            var phone="13693291433";
            mui.confirm('是否拨打'+phone+'?','提示',btnArray,function(e){
                if(e.index == 0){
                    plus.device.dial(phone,false);
                }
            });
        });
## 第二种：调用原生拨打电话，相对复杂一点，还需要区分ios和Android两个版本

        function call(number){
          if(plus.os.name=="Android"){
            var Intent = plus.android.importClass("android.content.Intent");
            var Uri = plus.android.importClass("android.net.Uri");
            var main = plus.android.runtimeMainActivity();
            var uri = Uri.parse("tel:"+number);
            var call = new Intent("android.intent.action.CALL", uri);
            main.startActivity(call);
        }else{
            //plus.device.dial(number, false);
            var UIAPP=plus.ios.importClass("UIApplication");
            var NSURL=plus.ios.importClass("NSURL");

            var app=UIAPP.sharedApplication();

            app.openURL(NSURL.URLWithString("tel://"+number));
        }
    }
