# Keyof Type Operator
The <b>keyof</b> type operator

The keyof operator takes an object type and produces a string or numeric literal union of its keys. The following type P is the same type as type P = "x" | "y":

```typescript
type Point = { x: number; y: number };
type P = keyof Point;
    
type P = keyof Point ```



Try

If the type has a string or number index signature, keyof will return those types instead:


```typescript 
type Arrayish = { [n: number]: unknown };
type A = keyof Arrayish;
    
type A = number
 
type Mapish = { [k: string]: boolean };
type M = keyof Mapish;
    
type M = string | number
```
Try

Note that in this example, M is string | number — this is because JavaScript object keys are always coerced to a string, so obj[0] is always the same as obj["0"].

keyof types become especially useful when combined with mapped types, which we’ll learn more about later.


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
