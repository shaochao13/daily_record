使用autobahn jar
```java
import de.tavendo.autobahn.WebSocketConnection;
import de.tavendo.autobahn.WebSocketException;
import de.tavendo.autobahn.WebSocketHandler;

private WebSocketConnection wsc;
@Override
    public void websocketconnect(final String msgText){
        if (wsc == null){
            wsc = new WebSocketConnection();
        }
        if (wsc != null && !wsc.isConnected()){
            try {
                wsc.connect(url, new WebSocketHandler(){
                    @Override
                    public void onOpen() {
                        LogUtils.i(TAG,"连接成功");
                        if (msgText != null){
                            //发送订阅请求
                            wsc.sendTextMessage(msgText);
                        }
                    }

                    @Override
                    public void onTextMessage(String payload) {
                        LogUtils.i(TAG, "onTextMessage");
                        LogUtils.i(TAG, payload);
                        try {
                            //在此处理返回的数据
                        } catch (AppException e) {
                            BaseWebSocketFragment.this.setStockDataBean(null);
                            e.printStackTrace();
                        }
                    }


                    @Override
                    public void onClose(int code, String reason) {
                        LogUtils.i(TAG, "close!!!!!!!!!!!!!!");
                    }
                });
            } catch (WebSocketException e) {
                e.printStackTrace();
            }
        }
    }

    @Override
    public void websocketreconnect(){
        websocketdisconnect();;
        websocketconnect(null);
    }

    @Override
    public void websocketdisconnect(){
        if (wsc != null && wsc.isConnected()){
            wsc.disconnect();
            wsc = null;
        }
    }

public void setSendMessageText(String smText) {
        LogUtils.i(TAG, sendMessageText);
        this.sendMessageText = smText;
        if (sendMessageText != null) {
            if (wsc != null && wsc.isConnected()){
                wsc.sendTextMessage(sendMessageText);
            }
            else{
                websocketconnect(this.sendMessageText);
            }
        }
    }

```