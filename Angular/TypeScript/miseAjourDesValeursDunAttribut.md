# Mettre à jour les attribut d'un objet dynamiquement 
imaginons t'as un objet color 
```ts
    export interface color{
        readonly red:number,
        readonly green:number,
        readonly blue :number
    }
```

et que t as un objet ou un signa de type color ,comment mettre à jour la valeur d'un attribut qui est contenue dans la variable canal='red' , sans changer la valeur des ancien attributs 
## réponse : on utilsie les attribut dynamique 
### dans le cas d'un signal 
```ts
    coulour.update((v)=>{
        ...v,
        [canal]=value
    })
```
### dans le cas d'une variable 
    ```ts
    var={
        ...var,
        [canal]:
    }
    ```

### remarque :
    dan le cas d'une variabl on aurait pu faire 

```ts
var[canal]=value
```
mais vu que les attributs sont readonly ,il faut créer un nouveau objet on copiant tout les attributs ...v