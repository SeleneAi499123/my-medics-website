# ASP.NET Web API

!!! info "下載及安裝 .net SDK"
    在建立第一支 web api 前，請先下載 [.NET Core](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks)，並安裝相關套件，支援跨平台。

---

## 建立 web api

在終端機輸入以下指令建立 web api 的檔案，並且啟動查看頁面。
```bash
dotnet new webapi -o my-web-api
dotnet watch run
```

!!! note "Note"
    .Net SDK 8.0 後的版本需要在後面加上 `-minimal=false`

---

## WeatherForecastController

找到 `/Controllers/WeatherForecastController.cs`，這是預設的 api 範例，裡面預設的 HttpGet 方法，決定 Client 端執行 get 動作時要回傳的值。

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

### Http 方法

| Method      | Description      |
| ----------- | ---------------- |
| `GET`       |  Fetch resource  |
| `PUT`       |  Update resource |
| `POST`      |  Insert data     |
| `DELETE`    |  Delete resource |


### 設定路徑名稱

`WeatherForecast` 繼承 `ControllerBase` 類別，要設定 api 的路徑，要在整個 fuction 的最上面修改 `[Route("路徑名稱")]`。

```cs
[ApiController]
[Route("wf")]
public class WeatherForecastController : ControllerBase
{
    //...
}
```



