# Template Driven Form

通常情況下，對於較簡單的表單，使用 Template Driven Form 較為方便和快速，表單的狀態和驗證邏輯都在 HTML 模板中指定，而響應式表單則更多地依賴於 TypeScript 程式碼。

---

## 初始化 Model 的值

因為不需要使用到 FormsGroup 來控制欄位，所以直接 new 一個物件當作初始值就好。

```ts title="Page2Component.ts"
export class Page2Component {
  capacity=["5","10","15","20"];
  meetingRoom:MeetingRoom;
  constructor (){
    this.meetingRoom=new MeetingRoom(101,'taiwan',this.capacity[1],true,true);
  }
  // 控制項驗證
  submitted=false;
  onSubmit(form:NgForm){
    if(form.valid){
      this.submitted=true;
    }
  }
}
```

---

## 表單元素設定

ngForm 是透過 `#` 來指向表單的欄位，表單用 `#form="ngForm"`，欄位用 `#input="ngModel"`。

```html hl_lines="1 4" title="Page2Component.html"
<form #form="ngForm" (ngSubmit)="onSubmit(form)">
    <div class="form-group">
        <label for="name">name</label>
        <input type="text" class="form-control" name="name" [(ngModel)]="meetingRoom.name" required #input="ngModel">
        <!--  自訂警示訊息 -->
        <div *ngIf="input.invalid" class="alert alert-danger">不可為空</div>
    </div>
    <div class="form-group">
        <label for="size">size</label>
        <select class="form-control" name="size" [(ngModel)]="meetingRoom.size">
            <option *ngFor="let c of capacity" [value]="c">{{c}}</option>
        </select>
    </div>
    <div class="form-group">
        <label for="projector">projector</label>
        <input type="checkbox" class="form-check-input" name="projector" [(ngModel)]="meetingRoom.projector">
    </div>
    <div class="form-group">
        <label for="tv">tv</label>
        <input type="checkbox" class="form-check-input" name="tv" [(ngModel)]="meetingRoom.tv">
    </div>
    <!-- 檢查輸入驗證，若未通過不可案按鈕 -->
    <button type="submit" class="btn btn-success" [disabled]="form.form.invalid">submit</button>
</form>
```

---

## 表單驗證
### 1. ngNativeValidate
在 `form` 元素內加上 `ngNativeValidate` 可以啟用 ngForm 預設的驗證提示，如下圖所示：

```html
<form #form="ngForm" (ngSubmit)="onSubmit(form)" ngNativeValidate>
```


### 2. 自訂驗證

通常 Template Driven Form 的表單欄位如果想要加人一些自訂的驗證，會用 [directive](../component/directive.md) 來做，以檢查分機號碼為例：

**a. 建立 directive**

```bash
ng g d checkExtNo
```
**b. 加入 provider**

```ts title="check-ext-no.directive.ts" hl_lines="5-7"
@Directive({
  selector: '[CheckExtNo]',
  providers:[
    {
        provide:NG_VALIDATORS,
        useExisting:CheckExtNoDirective,
        multi:true
    }
  ]
})
```

**c. 實作 Validator 介面**

```ts title="check-ext-no.directive.ts"
export class CheckExtNoDirective {
  validate(control:AbstractControl):ValidationErrors | null{
    let extNo:number=parseInt(control.value);
    let result=null;
    if(extNo<1000||extNo>1999){
      result={
        // CheckExtNo是指令名稱可自訂，裡面的兩個參數名稱也可以自訂
        "CheckExtNo":{
            actualValue:extNo,
            requiredValue:'分機介於1000~1999'
        }
      }
    }
    return result;
  }
}
```

**d. 套用到 HTML**
 
```html title=".html"
<div class="form-group">
    <label for="size">分機號碼</label>
    <input type="text" class="form-control" placeholder="租借者的辦公室分機號碼" required name="extNo" pattern="[0-9]{4}" title="4個數字" [(ngModel)]="rentRoom.extNo" #extNo="ngModel" CheckExtNo>
    <div *ngIf="extNo.invalid &&(extNo.dirty || extNo.touched)" class="alert alert-danger">
        <div *ngIf="extNo.errors?.['required']">請填寫分機</div>
        <div *ngIf="extNo.errors?.['pattern']">分機必須是數字四碼</div>
        <div *ngIf="extNo.errors?.['CheckExtNo']">{{extNo.errors?.['CheckExtNo'].requiredValue}}</div>
    </div>
</div>
```
