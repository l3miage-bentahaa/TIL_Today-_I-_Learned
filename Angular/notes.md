## pour avoir un signal visible dans la vue et la vue modéle
 ```ts
protected readonly signal_Name = signal<T> 
```
<br>

```ts
function isGhUserAvatarResponseP(data:unknow):Promise<Readonl<{avatr:string}>
    return GETgHuserResponseSchema.parseAsync(data);
```

une fonction qui recoit 

## clinet HTTP: 
    client réseau qui émet des requête avec le protocol http 


# Observable : 


```html
<img src={{this.avatarUrl()}}>
```

```ts
protected readonly avatarUrl:Signal<String>;


constructor(){
    const avatarUrl$:Observable<string>=avatarName.pipe(
        skip(1),
        debounceTime(1000),
        switchMap(name=>gettinAvatarUrl(this._http,name))
    )

    this.avatarUrl=toSignal(avatarUrl$,{initialValue:""})
}

```
