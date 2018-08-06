# 快速了解
	OSS支付SDK，主要打造微信支付，支付宝支付，以及其他银行支付接口标准库项目
	此项目以标准库的形式提供服务，也就是可以同时支持.Net Framework(4.6及以上版本) 和 .Net Core
如果有问题，也可以在公众号(osscoder)中提问:

![osscoder](http://7xil4i.com1.z0.glb.clouddn.com/osscoder_icon.jpg)

# OSS.PayCenter 使用
### 一. 安装使用
      nuget下安装命令：**Install-Package OSS.PaySdk.Wx**	（微信支付
      nuget下安装命令：**Install-Package OSS.PaySdk.Ali**	（支付宝支付

### 二. 调用示例

1. 微信调用示例：

```csharp
// 声明配置
private static WxPayCenterConfig config= new WxPayCenterConfig()
{
    AppId = "xxxxxxxxxx",
    MchId = "xxxxxxxxxx",
    Key = "xxxxxxxxxx",
    AppSecret = "xxxxxxxxxx",

    CertPassword = "xxxxxxxxxx",
    CertPath = "cert/xxxxxxxxxx.p12"   
};
//  公众号调用示例
private static WxPayTradeApi _api=new WxPayTradeApi(config);

public async Task<IActionResult> GetJsPayInfo()
{
    var order = new WxAddPayUniOrderReq
    {
        notify_url = "http://你的域名/wxpay/receive",
        body = "OSSCoder-测试商品",
        device_info = "WEB",
        openid = "oldRAw-Wu4eOD5CVPWeWVDOvhRbo",
        out_trade_no = "123456789",
        spbill_create_ip = "114.242.25.208",
        total_fee = 1,
        trade_type = "JSAPI"
    };
    
    var orderRes=await _api.AddUniOrderAsync(order);
    if (!orderRes.IsSuccess()) return Json(orderRes);

    var jsPara = _api.GetJsClientParaResp(orderRes.prepay_id);
    return Json(jsPara);
}
public IActionResult receive()
{
    string strPayResult;
    using (var streamReader = new StreamReader(Request.Body))
    {
        strPayResult = streamReader.ReadToEnd();
    }
    var payRes = _api.DecryptTradeResult(strPayResult);
    // to do something with payRes
    var returnXml = _api.GetCallBackReturnXml(new ResultMo());
    return Content(returnXml);
}
```

2. 支付宝调用示例

```csharp
 private static string privateKey = "自定义私钥";
 private static string publicKey = "支付宝提供的公钥";

protected static ZPayCenterConfig ZPayConfig { get; set; } = new ZPayCenterConfig()
{
    AppSource = "1",
    AppId = "xxxxxxxxxx",
    AppPrivateKey = privateKey,
    AppPublicKey = publicKey
};

protected static ZPayTradeApi zPayApi = new ZPayTradeApi(ZPayConfig);

public async Task<IActionResult> ZPay(PayOrderMo order)
{
    string orderNum = DateTime.Now.ToString("yyyyMMddHHmmss");

    var payReq = new ZAddPreTradeReq("http://pay.sample.osscoder.com/base/ZCallBack");

    payReq.body = order.order_name;
    payReq.out_trade_no = orderNum;
    payReq.total_amount = order.order_price;
    payReq.subject = order.order_name;

    var res =await zPayApi.AddPreTradeAsync(payReq);
    return Json(res);
}
```

### 三. 注意事项
	
	因为底层接口使用了Task返回，在.Net Framework MVC项目中如果你的在action中通过 Result或者wait等方式，直接返回ActionResult对象，界面会出现假死状态，解决方案：
	1. action 返回类型 ActionResult 修改为 async Task<ActionResult>, 全程异步
	2. 将异步调用方法 通过 var task=  Task.Run(()=> 异步方法 )返回异步对象，再使用task.Result即可