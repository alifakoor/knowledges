interface های همنام ادغام میشن
اما typeها اگر هم نام باشن خطا میده

---------------
interfaceها میتونن ارث بری کنن 
اما تایپ‌ها نمیتونن

------------
میشه به وسیله intersection یا همون &، یه تایپ جدید از اتصال چندتا تایپ ایجاد کرد
اما برای interfaceها نمیشه همچین چیزی داشت البته که میشه به صورت زیر یه تایپ جدید از چندتا interface ایجاد کرد
```ts
interface Teacher{
	name: string;
};

interface Student{
	name: string;
};

type  School = Teacher & Student;
```

همین قضیه برای unions یا همون | هم صادقه
```ts
interface Movie {
 name: string;
};

interface Music {
 name: string;
};

 type  Art = Movie | Music 
```

------------
یه تایپ میتونه یه تاپل باشه اما interface نه
```ts
type Characters = [string, number]
```

```ts
interface Characters {
	value: [string, number]
}
```
