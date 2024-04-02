```ts
function converter(meter: number | string): number {
    if (typeof meter === 'number') {
        return meter * 100;
    } else {
        return parseInt(meter) * 100;
    }
}
```
