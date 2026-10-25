# Notation topologique transdisciplinaire — v0.1

**Usage :** convertir une hypothèse formulée en français en proposition topologique testable.  
**Ce n’est pas une loi physique :** les symboles formalisent la structure de l’hypothèse; le modèle et les données doivent encore la tester.

## Alphabet minimal

| Symbole | Lecture | Sens topologique | Sens dans un cadre d’étude |
|---|---|---|---|
| `D` | domaine | couche d’objets | `Q` quantique, `G` géométrique/gravitationnel, `T` thermodynamique, etc. |
| `K_D=(V_D,Σ_D)` | complexe du domaine `D` | sommets `V_D` et simplex `Σ_D` encodent objets et relations déclarées | qubits/corrélations, régions/adjacences, états/échanges — selon la définition choisie |
| `Γ_AB` | liens entre couches `A,B` | arêtes ou simplexes reliant les deux complexes | relation interdisciplinaire; préciser : analogie, représentation ou couplage mesuré |
| `K_AB` | complexe joint | `Cl(K_A ⊔ K_B ∪ Γ_AB)`; `Cl` ajoute les faces nécessaires | système composé après insertion des liens `A–B` |
| `f_AB:K_A→K_B` | application de `A` dans `B` | transformation qui envoie les simplexes sur des simplexes | traduction/représentation précise; ne signifie pas, à elle seule, causalité physique |
| `H_k(K)` | homologie de degré `k` | classes de cycles qui ne sont pas des bords | structure globale de dimension `k` |
| `β_k(K)=rank H_k(K)` | nombre de Betti | nombre de classes indépendantes | `β₀` composants, `β₁` boucles, `β₂` cavités |
| `f_{AB*}` | action induite de `f_AB` | `H_k(K_A)→H_k(K_B)` | classes topologiques transportées par la représentation |
| `K^λ` | complexe au niveau `λ` | famille emboîtée `K^λ⊆K^μ` si `λ≤μ` | seuil, échelle, énergie, temps ou intensité — à préciser par le modèle |

**Base :** `H_k(K)=ker(∂_k)/im(∂_{k+1})`, avec `∂_k∂_{k+1}=0`. Une boucle n’est donc pas simplement un dessin fermé : c’est une classe qui ne se réduit pas à un bord dans le complexe choisi.

## Verbes d’hypothèse → formules

| Français précis | Formulation topologique |
|---|---|
| « Au moins une structure de dimension `k` de `A` survit dans `B`. » | `rank im(H_k(f_AB)) > 0` |
| « La traduction `A→B` ne perd aucune classe de degré `k`. » | `ker(H_k(f_AB)) = {0}` |
| « `A` et `B` ont la même topologie au degré `k`. » | `H_k(K_A) ≅ H_k(K_B)` — pas une équivalence physique complète |
| « Les liens entre `A` et `B` créent un nombre net positif de `k`-trous. » | `Δ_{Γ_AB}β_k := β_k(K_AB) − β_k(K_A ⊔ K_B) > 0` |
| « La structure apparaît à `λ_b` et disparaît à `λ_d`. » | intervalle de persistance `[λ_b, λ_d)` dans `K^λ` |

## Exemple : hypothèse quantique–gravitationnelle

**Phrase :** « Les corrélations quantiques, reliées aux adjacences géométriques, produisent une boucle globale absente des deux couches prises séparément. »

```text
K_Q  = complexe des relations quantiques déclarées
K_G  = complexe des adjacences géométriques déclarées
Γ_QG = liens proposés entre les deux couches
K_QG = Cl(K_Q ⊔ K_G ∪ Γ_QG)

Hypothèse :  Δ_{Γ_QG}β₁ > 0
```

**Lecture :** après ajout des liens quantique–géométrie, le complexe joint possède au moins une boucle indépendante de plus qu’avant. `Γ_QG` doit être défini par un modèle ou une mesure; une analogie seule ne suffit pas à l’appeler couplage physique.

Si l’hypothèse affirme plutôt qu’une boucle quantique est **représentée** par une boucle géométrique, on spécifie une application `f_QG` et on écrit :

```text
rank im(H₁(f_QG)) > 0
```

Les deux formules ne disent pas la même chose : la première teste une structure émergente dans l’assemblage; la seconde, le transfert d’une classe par une application.

## Chaîne de plusieurs disciplines

```text
K_Q  --f_QG-->  K_G  --f_GT-->  K_T
```

```text
rank im(H₁(f_GT ∘ f_QG)) > 0
```

Au moins une classe de boucle issue de la représentation quantique demeure non nulle après les deux traductions. Cela formalise une hypothèse de transfert; cela ne démontre ni que les applications existent physiquement, ni que la gravitation quantique est établie.

## Règle d’emploi

Toujours fixer : **(1)** ce que représentent les sommets et simplexes; **(2)** le type de `Γ` ou de `f`; **(3)** le degré `k`; **(4)** le critère numérique; **(5)** le test qui pourrait rendre la formule fausse.
