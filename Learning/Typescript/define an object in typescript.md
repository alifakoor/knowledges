1. Fixed Object:
```ts
let object:any = {
	name:'salar',
	age:18,
	country:'iran'
}
```

2. Index Signature:
```ts
let object:any = {};
object["name"] = "salar";
object["age"] = 18;
object["country"] = "iran";
```

تفاوت این دو در این است که fixed object در زمان کامپایل تعریف می‌شود، در حالی که با استفاده از index signature می‌توان در ران تایم پراپرتی جدید تعریف کرد.
در واقع استفاده از index signature باعث می‌شود که ابجکت ما داینامیک شود.