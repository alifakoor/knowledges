as const:
یک آرایه یا آبجکت را برای همیشه غیر قابل تغییر کنیم، به گونه‌ای که هیچ عضوی از آن کم نشود، یا نتوان به آن عضو جدیدی اضافه کرد.
```ts
const cars = ["Saab", "Volvo", "BMW"]  as const  ;
cars.push("Toyota");  // ❌ error 
cars = ["Toyota"]; // ❌ error 

//-----------

 const myCars = {                                                                 
 brand: 'Toyota',                                                           
 seats: 5
 } as const  ;
myCars.seats = 4 // ❌ Cannot assign to 'seats' because it is a read-only property. 
```

readonly:
```ts
function createCars(colors: readonly string[]) {
    colors.push('black');  // ❌ Error: Property 'push' does not exist on type 'readonly string[]'.
}

//-------

class Cars {
    readonly name: string
    constructor(name: string) {
        this.name = name
    }

    public setName(name: string) {
        this.name = name;  // ❌ Error: Cannot assign to 'name' because it is a read-only property.

    }

}
```

