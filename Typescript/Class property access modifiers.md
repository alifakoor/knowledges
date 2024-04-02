![[typescript_access_modifiers.png]]


معمولا قبل از پراپرتی‌های private از _ برای مشخص کردن اینکه این پراپرتی private است استفاده میکنیم
```ts
class Person {
    private _name: string;
    constructor(name: string) {
        this._name = name;
    }

    private showingName(): void {
        console.log(`my name is ${this._name}`);
    }  
}

const personOne = new Person("mahan");

console.log(personOne.name); // ❌ Property 'name' is private and only accessible within class 'Person'

console.log(personOne.showingName()); // ❌ Property 'showingName' is private and only accessible within class 'Person'
```

متدهای getter و setter برای پراپرتی‌های private
```ts
class Person {
    private _name: string;
    constructor(name: string) {
        this._name = name;
    }

    get userName(): string {
        return this._name;
    } 

    set userName(value: string) {
        this._name = value;
    } 
}

const personOne = new Person("mahan");

console.log(personOne.userName); // mahan

personOne.userName = "mamad";

console.log(personOne.userName); // mamad
```



