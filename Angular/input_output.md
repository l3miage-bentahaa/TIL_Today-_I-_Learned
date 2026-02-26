# input output
## input
on peut définir un input d'un type <T> dans un composant A , lorsqu'on utilise le composant A dans le composant B , les attributs du composant A :

## output
quand on définit un output dans un composant ,on doit emmetre ça valeur pour qu'elle soit visible 


```html
<app-A [input]="objetDeTypeT"></app-A>
```

exemple amélioré :


```ts
import { Component, computed, input, output } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { Etablissement } from '../../data/Etablissement';
import { MatCardModule } from '@angular/material/card';
import { MatChipsModule } from '@angular/material/chips';
import { FiltreConfig } from '@data/Filtre.defs';

@Component({
  selector: 'app-etablissement',
  imports: [
    FormsModule,
    MatCardModule,
    MatChipsModule
  ],
  templateUrl: './etablissement.component.html',
  styleUrl: './etablissement.component.scss'
})
export class EtablissementComponent {
  public readonly data = input.required<Etablissement>();
  public readonly updateFilter = output<FiltreConfig>();
  public readonly myInput=input.required<number>();


  /**
   * Partie 1 : Définir le signal dérivé nombreTotalEleves.
   * Renvoie une string contenant les effectifs totaux connus de l'établissement,
   * sous la forme "effectif(année), effectif(année), ...".
   * Par exemple : "500(2018), 520(2019), 530(2020)"
   */

  public nombreTotalEleves=computed<string>(
    ()=>{
      let resultat=""
      this.data().nombreTotalEleves.forEach((v)=>
        resultat=resultat+v.effectif+"("+v.année+")"
      )
      return resultat;
    }
  )

  
  /**
   * Partie 1 : Définir le signal dérivé labelRep, qui renvoie "REP", "REP+", ou undefined.
   */

  public labelRep=computed<"REP" | "REP+"| undefined>(
    ()=>{
      if(this.data().rep){
        return "REP"
      }
      else if(this.data().repPlus){
        return "REP+"
      }
      else{
        return undefined
      }
    }
  )


  /**
   * Partie 1 : Définir le signal dérivé imageTypeEtablissement, qui renvoie le chemin de l'image selon le niveau (collège ou lycée).
   * - Pour le niveau collège, renvoyer 'assets/college.jpeg'
   * - Pour le niveau lycée, renvoyer 'assets/lycée.png'
   * - Si on ne peut pas déterminer le niveau, renvoyer 'assets/inconnu.png'.
   */


  public imageTypeEtablisssement =computed<string>(
    ()=>{
      return 'assets/'+this.data().typeEtablissement.toLowerCase()+'.jpeg'
    }
  )





}

```
 ```html
 <mat-card appearance="outlined">
  
  <mat-card-header>
    <mat-card-title-group>
      <mat-card-title>{{ data().patronyme }}</mat-card-title>
      <mat-card-subtitle>{{ data().typeEtablissement }}</mat-card-subtitle>
      <img mat-card-sm-image src="{{imageTypeEtablisssement()}}" />
      
    </mat-card-title-group>
  </mat-card-header>

  <mat-card-content>
    <p>Nombre d'élèves : {{this.nombreTotalEleves()}} </p>
    <pre>min {{this.data().effectifMin}} -- max {{this.data().effectifMax}}</pre>
    <mat-chip-set>
      <!-- Afficher ici le secteur, la commune, le département et le label REP
           à l'aide de composants mat-chip.
           Quand une puce est cliquée, émettre un évènement via updateFilter
      -->

        <mat-chip (click)="updateFilter.emit({secteur:this.data().secteur})">{{this.data().secteur}}</mat-chip>
        <mat-chip (click)="updateFilter.emit({commune:this.data().commune})"> {{this.data().commune}}</mat-chip>
        <mat-chip (click)="updateFilter.emit({departement:this.data().departement})"> {{this.data().departement}}</mat-chip>
        <mat-chip (click)="updateFilter.emit({REP:this.labelRep()})"> {{ this.labelRep()}}</mat-chip>

        <p>le nombre dans mon input est {{myInput()}}</p>
      
    </mat-chip-set>
  </mat-card-content>

</mat-card>

 ```