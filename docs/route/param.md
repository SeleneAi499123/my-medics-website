# 參數的傳遞

##  定義參數名稱

我們可以在路由的`path`屬性定義參數名稱，在參數名稱前加上冒號`:`，如`:id`, `:state`。

```typescript title="app-routing.module.ts" hl_lines="3"
{
    path:'product', component:'ProductComponent', children:[
        { path:':id', component:'ProductDetailComponent'}
    ]
}
```

---

## 傳送參數


=== "router.navigate"

    ```ts hl_lines="4" title="product.component.ts"
    constructor(private router:Router){}
    goProduct(id:number){
        // 以路徑段陣列表示
        this.router.navigate(['/','product',id]);
    }
    ```

=== "router.navigateByUrl"

    ```ts hl_lines="4" title="product.component.ts"
    constructor(private router:Router){}
    goProduct(id:number){
        // 以字串表示
        this.router.navigateByUrl(`/product/${id}`);
    }
    ```





---

##  接收參數

在子路由內的`ngDoCheck()`獲取參數值。

```ts title="product-detail.component.ts" hl_lines="2 3"
constructor(private route:ActivatedRoute){}
ngDoCheck(){
    let value=this.route.snapshot.paramMap.get('id');
    this.id=Number(value);
}

```