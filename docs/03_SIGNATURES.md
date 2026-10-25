# 03 — Signatures : séparer les sens de `P_sig`

`P_sig` est conservé comme **nom d’origine des dépôts**. Dans la langue canonique, chaque sens reçoit son propre nom. Aucun nombre sous l’étiquette source `P_sig` n’est comparable à un autre tant que sa construction n’est pas identique.

## Types canoniques et réductions source repérés

| Type canonique | Construction | Dépôts où ce sens est repéré | Ce que le type mesure |
|---|---|---|---|
| `L₁^max(K)` | maximum des longueurs des intervalles H1 finis | ODV-AEON/TTF, `Travaux`, plugin LeWM, graphe du Topological Studio, Skynet, Cyber, `synchrotron-24`, `Ratiss-Jonathan-Labs` | durée de la classe H1 finie la plus longue dans une filtration donnée |
| `L₁^sum(K)` | somme des longueurs H1 finies | `metac-bot-template/ratiss_brain/topology_real.py`; solveur AEON/Fusion quand GUDHI est disponible | masse cumulée des classes H1 finies; différente du maximum |
| `L_{1,2}^{sum,>δ}(K)` | sommes de persistance H1 et H2 au-dessus d’un seuil | conteneur `synchrotron-24` | persistance totale multi-degrés; distincte de `L₁^max` |
| `S_bio` | `1−exp(−(L₁^{sum,>1Å}+1,5L₂^{sum,>1Å})/(15·max(1,N)))` | RATISS-Bio | agrégat H1/H2 normalisé; pas un maximum H1 |
| `S_neuro(t)` | score H1 normalisé par fenêtre Takens | RATISS-NEURO | série bornée `[0,1]`; formule source spécifique ci-dessous |
| `S_sub0(f,G)` | plus longue durée finie H0 sous-niveau, divisée par l’étendue du champ | RATISS-NEURO | score distinct de la persistance H1 de Takens |
| `S_Bloch` | moyenne temporelle du rayon du vecteur de Bloch | RATISS-QPU-AMBIENT | indicateur géométrique de pureté/cohérence, **pas** une persistance homologique |
| `N_vort^{gate}` | nombre de vortex de phase détectés sous un seuil d’amplitude | RATISS-PHOTON | singularités de phase locales; distinctes de H1 persistant |
| `S_graph^{?}` | `P_sig` sur association de comptages QPU | QPU-Ratiss-COSMOS | `P_sig` graphique et sidecar logique séparés; réducteur exact à versionner |
| `S_risk^{topo}` | score de risque topologique borné annoncé 0–100 | RATISS Aeon Prime | score de surface d’attaque; formule de réduction non exposée dans le README consulté |
| `S_logical(t)` | sortie du noyau de qubit logique simulé | Topological Studio, QPU-COSMOS, banc Grover | signal logiciel/sidecar; ne pas l’assimiler à l’homologie du graphe ou à l’état QPU |
| `N₁^TTF(K)` | estimateur source de « bruit H1 » | ODV-AEON/TTF | médiane des durées si plus de deux classes; sinon 0,1 × la plus courte durée; `1` si aucune classe finie |
| `A_τ^norm(s)` | aire absolue du cycle du plongement retardé, divisée par la taille de fenêtre et la variance | RATISS-GRID | forme/aire d’une trajectoire retardée; **pas** le calcul d’une persistance H1 |
| `Γ_{XY}^phase(t)` | relation de verrouillage de phase entre couches | glossaire/théorie FOCAL | synchronisation entre couches; formule scalaire non spécifiée par la définition consultée |
| `S_robust` | score combiné `L₁^max` seuillé + corrélation de bord − poids × entropie | `Travaux` | décision combinée; pas un invariant topologique pur |

### 1. Durée maximale H1

Pour les intervalles finis `I_j^1=[b_j,d_j)` du diagramme H1 :

```text
L₁^max(K) = max_(j∈I_{1,fin}) (d_j − b_j)
```

Aucun intervalle fini donne `0` selon les implémentations consultées. La valeur dépend du nuage, de la distance, de la filtration, du seuil maximal et de la méthode de réduction. Dans `synchrotron-24`, le champ source nommé `H1` est explicitement calculé comme `max(d_j−b_j)` par `ripser` sur le nuage des positions : la traduction est `L₁^max(K_t)`, **pas** le nombre de Betti `β₁`. Un nombre flottant comme `H1=5,296` est donc une durée de persistance dans les unités/échelles du calcul, non un Betti fractionnaire.

### 2. Persistance totale H1

```text
L₁^sum(K) = Σ_j (d_j − b_j)
```

Cette somme n’est pas la durée de la plus longue classe. Le moteur `metac-bot-template` la calcule comme score interne après normalisation L2 et réduction de Vietoris–Rips sur F₂. Dans son implémentation, les classes encore vivantes au seuil `max_edge` sont terminées à ce seuil : la somme inclut donc des durées censurées par la coupure. Le conteneur de `synchrotron-24` emploie une autre réduction : somme des longueurs finies H1 **et** H2 dépassant `δ=0,05`, sans normalisation; elle se note `L_{1,2}^{sum,>δ}` et ne se réduit pas à un score H1 seul.

### Réducteurs biomoléculaires et multi-degrés

Dans RATISS-Bio, le code conserve les diagrammes H0, H1 et H2, somme les longueurs **finies** dont la persistance dépasse `1 Å`, puis combine H1 et H2 :

```text
T_k = Σ_(j : ℓ_j^k > 1 Å) ℓ_j^k
S_bio = 1 − exp(−(T₁ + 1,5·T₂)/(15·max(1,N)))
```

Le calcul de diagrammes est tronqué à `maxdim=2`, au seuil de Rips `30 Å`, et sous-échantillonne à 220 points si nécessaire; la normalisation emploie le nombre d’entrée `N`. C’est un agrégat H1/H2 propre à cette implémentation, pas `L₁^max`. Le README décrit aussi des nuages protéiques Cα, tandis que le module fournit un constructeur de nuage d’ADN : l’objet d’entrée doit être cité par expérience.

Le conteneur `synchrotron-24` utilise `L_{1,2}^{sum,>δ}` : somme non normalisée des longueurs finies H1 et H2 dépassant `δ=0,05`. Les sorties nommées `H1` dans les scénarios S03/S05 sont en revanche `L₁^max` d’un nuage de positions.

### Score neuro-temporel sur un embedding de Takens

RATISS-NEURO calcule, pour chaque fenêtre, un score source H1 borné :

```text
ℓ_j = d_j − b_j sur les barres H1 finies
m   = nombre de barres H1 finies
S_neuro(w) = clip( Σ_j ℓ_j/(m·max_j ℓ_j + 10⁻¹²) − 1/m, 0, 1)
P_sig^neuro(t) = S_neuro(w_t)
```

La fenêtre est centrée-réduite, plongée par Takens (`dim=3`, `delay=8` échantillons), puis limitée à 120 points; réglages consultés : `window=0,5 s`, `hop=0,05 s`. Le pic temporel est le maximum des scores de fenêtres. Le code rapporte en plus une durée moyenne H1 convertie en millisecondes et un compte maximal de barres H2 finies lorsque l’échantillon permet le calcul H2 : ces champs restent distincts de `S_neuro`.

Un autre module neuro calcule sur un graphe seuillé de corrélations des neurones sentinelles un masque de synapses via les arêtes hors-arbre de Kruskal. Pour le **graphe seul** (complexe de dimension 1), le proxy de cycles correspond au rang cyclomatique `|E|−|V|+c`; ce n’est pas une filtration persistante de Vietoris–Rips ni le H1 d’un complexe cliquique où des triangles peuvent remplir les cycles.

Dans l’ancienne formule LCT, le code TTF construisait aussi `N₁^TTF(K)` : médiane des durées si plus de deux classes; sinon 0,1 × la plus courte durée; `1` s’il n’y a aucune classe. Le ratio historique est donc `R_old=L₁^max/(N₁^TTF+ε)`. Le code le déclare non monotone et ne le garde pas comme métrique principale.

### 3. Aire de Takens

Pour le nuage retardé `Delay_τ(s)=((x_i,y_i))`, avec `x_i=s_i` et `y_i=s_(i+τ)`, la construction GRID est :

```text
A_τ^norm(s) = | ½ Σ_i (x_i y_(i+1) − x_(i+1) y_i) |
              / (n Var(s) + ε)
```

L’aire absolue est normalisée; l’orientation est perdue. Cette formule ne produit pas un diagramme de persistance.

### Vortex de phase — RATISS-PHOTON

Le protocole de `RATISS-PHOTON` compte des singularités locales pour lesquelles le winding de `arg(ψ)` autour d’une plaquette vaut `+2π` ou `−2π`, avec un gate d’amplitude afin d’écarter les faux vortex des zones sombres. On le note `N_vort^{gate}`. Il s’agit d’un comptage de défauts de phase, pas du nombre `β₁` d’un espace ni du nombre d’intervalles H1 persistants. Le symbole source `H1` du dépôt désigne aussi une hypothèse (« support physique de la probabilité »), non l’homologie H1.

### 4. Synchronisation inter-couches

Lorsque `P_sig(X↔Y)` signifie « phase-locking entre couches », le dictionnaire l’écrit comme relation `Γ_{XY}^phase(t)`. Si une valeur scalaire est nécessaire, le dépôt doit spécifier le calcul, l’intervalle, les unités et les contrôles avant de la comparer à une durée H1.

### 5. Rayon moyen de Bloch — QPU-AMBIENT

Le code de RATISS-QPU-AMBIENT définit `P_sig` sur une trajectoire de Bloch comme :

```text
S_Bloch = moyenne_i ||r⃗(t_i)||
```

où `r⃗` est le vecteur de Bloch obtenu de la matrice densité. Le code l’interprète comme un indicateur géométrique de pureté/cohérence (surface pour un état pur, centre pour un état maximalement mixte). Malgré le nom source et l’image de la sphère, il ne calcule ni diagramme de persistance ni groupe d’homologie.

### 6. Champs distincts dans les studios quantiques

Le contrat du Studio sépare :

```text
topology.psig       → L₁^max(K_graph)
logical_topology    → S_logical(t)
tsp_inspection.path → Path_G(…)
```

Ce sont respectivement une signature de persistance du graphe, une sortie du noyau logique et une route d’inspection. Une route TSP n’est pas une classe H1.

## Correspondance des usages sources

| Écriture historique | Écriture du dictionnaire | Remarque |
|---|---|---|
| `P_sig = longest finite H1 persistence` | `L₁^max(K)` | même construction, alias remplacé |
| `P_sig = sum of H1 lifetimes` | `L₁^sum(K)` | autre réduction du diagramme |
| RATISS-Bio `P_sig` combinant H1/H2 et une exponentielle | `S_bio` | poids H2=1,5; seuil de persistance >1 Å; normalisation propre au code |
| RATISS-NEURO `P_sig^neuro(t)` | `S_neuro(t)` | score H1 par fenêtre Takens; durées H1/H2 en champs séparés |
| QPU-AMBIENT `P_sig` de trajectoire Bloch | `S_Bloch` | moyenne du rayon Bloch; géométrique, pas homologique |
| RATISS-PHOTON vortex `±2π` | `N_vort^{gate}` | winding local filtré par amplitude; pas un Betti |
| `P_sig = normalized Takens cycle area` | `A_τ^norm(s)` | géométrie de trajectoire, pas homologie |
| `P_sig(X↔Y)=phase-locking` | `Γ_{XY}^phase(t)` | relation inter-couches, définition numérique à compléter |
| `logical_topology.P_sig` | `S_logical(t)` | signal algorithmique distinct |
| `P_sig` sans méthode déclarée | `S_topo^{?}` | signature topologique non typée; ne pas utiliser pour comparer |

## Note documentaire : GRID

Le README de GRID parle de `P_sig`, H1 et Vietoris–Rips; le fichier d’implémentation `ratiss_grid/topology.py` calcule une aire de Takens, et `MEMO_GRID.md` précise que l’aire est utilisée **à la place** d’un H1 Vietoris–Rips naïf. Cette édition canonise l’implémentation comme `A_τ^norm` et conserve la divergence du README comme point documentaire à harmoniser.
