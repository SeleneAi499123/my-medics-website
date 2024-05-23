# Entity Framework

Entity Framework 是由 Microsoft 開發的 ORM 框架，用於在應用程序和數據庫之間建立映射，從而使開發人員能夠使用 .NET 對象來處理數據庫操作，而不需要直接處理 SQL 語句，它支援多種資料庫，包括 SQL Server、MySQL、Oracle 等。

---

## 安裝 Entity Framework Core

```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools
dotnet add package Microsoft.EntityFrameworkCore.Design
```

---

## 定義資料模型

建立 Models 目錄來放資料模型 `Models/MeetingRooms.cs`。

```cs title="MeetingRooms.cs"
using System.ComponentModel.DataAnnotations.Schema;
using Microsoft.EntityFrameworkCore;

public class MeetingRoom{
    public int ID{get;set;}
    [Column(TypeName ="nvarchar(30)")]
    public string Name{get;set;}
    public int Size{get;set;}
    public bool? Projector{get;set;}
    public bool? TV{get;set;}
}

public class MeetingRoomContext:DbContext{
    public MeetingRoomContext(DbContextOptions<MeetingRoomContext> options):base(options){}
    public DbSet<MeetingRoom> MeetingRoomDbSet{get;set;}
}
```

---

## 初始化 DbContext 資料內容

在 Models 資料夾內加入 `DbInitializer.cs`。

```cs title="DbInitialize.cs"
namespace my-web-api.Models;
// namespace 表示此檔案可以給外部using

public static class DbInitializer
{
    public static void Initialize(MeetingRoomContext context){
        context.Database.EnsureCreate();
        // 如果已有初始資料則不需初始化;
        if(context.MeetingRoomDbSet.any())[
            return;
        ]
        MeetingRoom mrList[]={
            new MeetingRoom{
                Name="tiawn",
                Size=10,
                Projector=true,
                TV=true,
            },
            // ... 以下省略
        };
        context.MeetingRoomDbSet.AddRange(mrList);
        context.SaveChanges();
    }
}
```

---

## 設定連線字串

```json title="appsetting.json"
"ConnectionStrings": {
    "MeetingDB": "Server=.\\sqlexpress;Database=MeetingRoomDB; Integrated Security=True;TrustServerCertificate=true;MultipleActiveResultSets=True;"
},
```

!!! warning "Warning"
    這裡設定`Integrated Security=True`是因為只在本地資料庫上進行操作，實際情況會有使用者帳密。


---

## 修改 Program.cs

```cs title="Program.cs"
using Microsoft.EntityFrameworkCore;
using my-web-api.Models;

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddDbContext<MeetingRoomContext>(
    optuins=> options.UseSqlServer(
        builder.Configuration.GetConnectionString("MeetingDB");
    )
);
```

---

## 初始化資料表內容

```cs title="Program.cs" hl_lines="3-7"
if (app.Environment.IsDevelopment())
{
    using(var scope=app.Service.CreateScope()){
        var service= scope.ServiceProvider;
        var context= service.GetRequiredService<MeetingRoomContext>();
        DbInitializer.Initialize(context);
    }
    app.UseSwagger();
    app.UseSwaggerUI();
}
```

---

## 更新資料庫

```bash
dotnet build
dotnet tool install --global dotnet-ef
dotnet ef migrations and InitailCreate
dotnet ef database update
```

---

## 自動產生 api controller

```bash
dotnet aspnet-codegenerator controller -name MeetingRoomsController -async -api -m MeetingRoom -dc MeetingRoomContext -outDir Controllers
```

!!! info "安裝 aspnet 程式產生器"
    ```
    dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design  
    dotnet tool install -g dotnet-aspnet-codegenerator
    ```

---

## 建構時初始化 DbContext

```cs title="MeetingRoomsController.cs"
public class MeetingRoomsController:ComtrollerBase{
    private readonly MeetingRoomContext _context;
    public MeetingRoomsController(MeetingRoomContext _context){
        _context=context;
    }
}
```