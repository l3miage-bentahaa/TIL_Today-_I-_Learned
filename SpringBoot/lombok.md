# Annotations Lombok les plus utiles

## Introduction

**Lombok** est une bibliothèque Java qui permet de **réduire le code répétitif (boilerplate)** en générant automatiquement certaines parties du code lors de la compilation.  
Elle est très utilisée dans les projets Java modernes, notamment avec **Spring Boot** et **Hibernate**.

Lombok fonctionne grâce à des **annotations** placées sur les classes, les attributs ou les constructeurs.

---

# 1. `@Getter`

## Principe

L'annotation `@Getter` génère automatiquement les **méthodes d'accès (getters)** pour les attributs d'une classe.

## Exemple

```java
import lombok.Getter;

@Getter
public class User {

    private long id;
    private String name;
    private String email;

}