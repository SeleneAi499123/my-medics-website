# Reactive Form

響應式表單是一種能夠根據使用者設備的大小和類型自動調整其佈局和外觀的表單。這種表單可以在桌面電腦、平板電腦和手機等各種設備上提供最佳的使用體驗，確保用戶能夠輕鬆地填寫和提交表單。


## 引用模組

想要建立一個響應式表單，需要先在專案內匯入`ReactiveFormsModule`才能使用相關功能。

```ts title="app.module.ts" hl_lines="1 10"
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    // ...
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    ReactiveFormsModule,
  ],
  //...
})
```

## 建立類別

遵循 MVC 的網頁結構，我們會需要一個類別來儲存表單內的所有欄位資料，首先使用Angular CLI建立一個類別，並在類別裡定義欄位名稱及屬性。

```bash
ng g cl MeetingRoom
```

```ts title="meeting-room.ts"
export class MeetingRoom {
    constructor(
        public id: number,
        public name: string,
        public size: string,
        public projector?: boolean,  // 問號表示可為null
        public tv?: boolean          // 問號表示可為null

    ){}
}
```

## 使用 FormBuilder

我們可以在表單建構的時候使用`FormGroup`的`FormBuilder`來定義欄位名及屬性，然後在`ngOnInit()`時使用`setValue()`來設值。

```ts hl_lines="3 6 8-13 18"
export class Page1Component {
  capacity=["5","10","15","20"];
  meetingRoomForm: FormGroup;
  meetingRoom: MeetingRoom;

  constructor (builder:FormBuilder){
    this.meetingRoom=new MeetingRoom(101,'taiwan',this.capacity[1],true,true);
    this.meetingRoomForm=builder.group({
      'id':['',[Validators.required]],
      'name':['',[Validators.required]],
      'size':[''],
      'projector':[''],
      'tv':['']
    })
  }

  ngOnInit(): void {
    this.meetingRoomForm.setValue(this.meetingRoom);
  }

  onSubmit(){
    this.meetingRoom=this.meetingRoomForm.value;
  }
}
```

## 設定表單元素的property

在表單的設計上，需要在`<form>`元素內設定`[formGroup]="meetingRoomForm"`以及`(ngSubmit)="onSubmit()">`，以及針對欄位元素設定`formControlName="name"`來進行表單資料的binding。

```html hl_lines="1 4 8 14 18 20"
<form [formGroup]="meetingRoomForm" (ngSubmit)="onSubmit()">
    <div class="form-group">
        <label for="name">name</label>
        <input type="text" class="form-control" formControlName="name">
    </div>
    <div class="form-group">
        <label for="size">size</label>
        <select class="form-control" formControlName="size">
            <option *ngFor="let c of capacity" [value]="c">{{c}}</option>
        </select>
    </div>
    <div class="form-group">
        <label for="projector">projector</label>
        <input type="checkbox" class="form-check-input" formControlName="projector">
    </div>
    <div class="form-group">
        <label for="tv">tv</label>
        <input type="checkbox" class="form-check-input" formControlName="tv">
    </div>
    <button type="submit" class="btn btn-success">submit</button>
</form>
```

## 表單驗證
