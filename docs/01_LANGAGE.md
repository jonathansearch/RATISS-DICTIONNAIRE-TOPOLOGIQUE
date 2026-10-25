# 01 — Langage topologique RATISS

**Objet :** une notation mathématique transdisciplinaire, non un langage d’exécution. Les symboles disent *quel objet on construit, quelle relation on pose et quelle structure topologique on suit*. Ce document développe la grammaire du dictionnaire à partir du socle accepté [00 — Notation transdisciplinaire v0.1](00_NOTATION_TOPOLOGIQUE_TRANSDISCIPLINAIRE_V0_1.md), dont la copie incluse est verbatim.

## 1. Domaine et structure

Un domaine porte un indice : `Q` quantique, `G` géométrique/gravitationnel, `T` thermodynamique, `I` information, `N` réseau, `L` latent/IA. L’indice est une étiquette de contexte, pas une loi.

```text
V_D                 objets du domaine D
G_D = (V_D, E_D)    graphe de relations déclarées
K_D = (V_D, Σ_D)    complexe simplicial du domaine D
X_D                 espace ou nuage géométrique du domaine D
```

- **Graphe** : liens par paires. Les relations peuvent être dirigées, non dirigées, pondérées et typées.
- **Complexe simplicial** : liens de plusieurs éléments à la fois. Chaque simplex contient aussi toutes ses faces.
- **Nuage/espace** : points munis d’une distance ou d’une topologie déclarée.

`G_D` et `K_D` ne sont pas interchangeables : le second peut coder des relations d’ordre supérieur, et ses homologies dépendent de la construction choisie.

## 2. Relier plusieurs domaines

```text
Γ_AB^r ⊆ V_A × V_B       relations entre les couches A et B, de type r
K_(A⋈B) = Cl(K_A ⊔ K_B ∪ Γ_AB^r)   complexe conjoint après ajout des liens
f_AB : K_A → K_B          application structurelle déclarée
f_AB* : H_k(K_A) → H_k(K_B) application induite sur les classes de degré k
```

`r` précise le rôle du lien : `assoc` association, `seq` succession orientée, `phase` relation de phase, `ana` analogie, `obs` interaction mesurée. `τ` reste réservé au retard temporel de `Delay_τ`. Une analogie n’est pas un couplage physique.

- Employer `Γ_AB^r` lorsqu’il existe des relations nombreuses ou plusieurs-à-plusieurs.
- Employer `f_AB` lorsqu’une règle de traduction de chaque structure de A vers B est définie.
- Un `f_AB` représente une correspondance mathématique; il n’affirme pas à lui seul une causalité.
- `Cl` ajoute les faces requises pour obtenir un complexe valide.

Pour plusieurs couches, les liens et applications se composent en chaîne. Exemple de forme, non d’hypothèse nouvelle :

```text
K_Q → K_G → K_T
(f_GT ∘ f_QG)* = f_GT* ∘ f_QG*
```

## 3. Trouver les structures topologiques

```text
∂_k : C_k(K) → C_(k−1)(K)      bord d’une chaîne de dimension k
∂_(k−1) ∘ ∂_k = 0             le bord d’un bord est nul
H_k(K) = ker(∂_k) / im(∂_(k+1)) classes de cycles qui ne sont pas des bords
β_k(K) = rank H_k(K)            nombre de classes indépendantes
```

Lecture usuelle : `H₀` / `β₀` composantes; `H₁` / `β₁` boucles; `H₂` / `β₂` cavités ou enveloppes fermées. Le sens exact dépend de la représentation et du degré maximal calculé.

```text
χ(K) = Σ_k (−1)^k β_k(K)        caractéristique d’Euler
```

Un nombre de Betti est un invariant de l’objet construit — pas directement une mesure d’énergie, de phase ou de causalité.

## 4. Échelle et persistance

```text
K^λ₁ ⊆ K^λ₂, si λ₁ ≤ λ₂     filtration croissante
D_k(K^λ)                      diagramme d’intervalles de degré k
[b_j, d_j)                    naissance et disparition d’une classe
β_k(K^λ)                      classes de degré k présentes à l’échelle λ
N_{k,fin}^{bars}              nombre d’intervalles finis du diagramme complet
L_k^max = max_(j fini)(d_j − b_j) durée finie maximale au degré k
L_k^sum = Σ_(j fini)(d_j − b_j) somme des durées finies au degré k
```

`λ` peut représenter une distance, un seuil, un bruit, un temps ou un couplage, **mais son type et son unité doivent être indiqués**. `β_k(K^λ)` compte les classes présentes à un niveau fixé; `N_{k,fin}^{bars}` compte les intervalles finis sur tout le diagramme. Ce ne sont pas des mesures interchangeables. Les classes infinies sont exclues des durées finies, sauf définition particulière.

Pour le complexe de Vietoris–Rips : `VR_ε(X)` relie les points séparés par au plus `ε`; tout groupe dont les distances deux à deux respectent le seuil forme un simplex. La famille `VR_ε(X)` quand `ε` augmente est une filtration.

## 5. Formes particulières déjà utilisées

```text
Delay_τ(s) = {(s_i, s_(i+τ))}   plongement à retard d’un signal
A_τ^norm(s)                       aire normalisée de sa trajectoire 2D
Hol_γ                          phase géométrique accumulée le long d’un chemin fermé γ
Path_G(u,v)                    chemin dans un graphe entre u et v
```

`A_τ` et `Hol_γ` ne sont pas des homologies. Le dictionnaire les garde comme signatures géométriques ou de phase, distinctes de `L_k^max`.

## 6. Forme d’une entrée dans la langue

Chaque entrée mathématique se lit avec les champs suivants :

```text
[domaine ; objet ; relations ; opération topologique ; degré/échelle ; statut]
```

Exemple de squelette : ` [Q ; K_Q ; Γ_QG^obs ; H₁ ; λ ; hypothèse ] `.

Ce cadre évite de confondre une représentation, un lien mesuré et une équivalence topologique. Les formules propres à une nouvelle hypothèse seront ajoutées quand l’hypothèse sera travaillée.