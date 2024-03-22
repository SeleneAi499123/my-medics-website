#  ASP.NET Web API

ASP.NET Web API 是一個由 Microsoft 開發的框架，用於建立和提供 Web 服務。它通過 HTTP 協議來提供數據和服務，並且能夠與各種客戶端（如網頁應用程序、移動應用程序等）進行通信。ASP.NET Web API 提供了許多功能，包括路由、模型繫結、序列化、授權和驗證等。

!!! info "下載及安裝 .net SDK"
    在建立第一支 web api前，請先到官方網站安裝相關套件：https://dotnet.microsoft.com/en-us/download/visual-studio-sdks，`.NET Core`支援跨平台。

## 建立 web api

在終端機輸入以下指令建立web api的檔案，並且啟動查看頁面。
```bash
dotnet new webapi -o my-web-api
```

```bash
dotnet watch run
```

!!! note "Note"
    .Net SDK 8.0 後的版本需要在後面加上 `-minimal=false`

## WeatherForecastController

使用指令建立的api，可以找到`/Controllers/WeatherForecastController.cs`，這是預設的api範例，裡面預設的HttpGet方法，決定Client端執行get動作時要回傳的值。

### Http方法

=== "多參數傳遞"

    ```cs
    [HttpGet("{year}/{month}/{day}")]
    public ActionResult<string> Get(int year,int month,int day){
        return (new DateTime(year,month,day)).ToString();

    }
    ```

=== "單一參數傳遞" 

    ``` cs
    private static readonly string[] Summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };

    [HttpGet("{id}")]
    public ActionResult<string> Get(int id){
        if(id>Summaries.Length){
            return NotFound();
        }
        else{
            return Summaries[id];
        }        
    }
    ```

| Method      | Description      |
| ----------- | ---------------- |
| `GET`       |  Fetch resource  |
| `PUT`       |  Update resource |
| `POST`      |  Insert data     |
| `DELETE`    |  Delete resource |


### 設定路徑名稱

WeatherForecast繼承`ControllerBase`類別，要設定api的路徑，要在整個fuction的最上面修改`[Route("路徑名稱")]`。

```cs
[ApiController]
[Route("wf")]
public class WeatherForecastController : ControllerBase
{
    //...
}
```



