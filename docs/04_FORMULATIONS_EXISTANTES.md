# 04 — Formulations topologiques déjà présentes dans RATISS

**Règle :** la colonne « langue RATISS » traduit les objets et les relations des sources. Elle n’ajoute pas une nouvelle hypothèse. Les statuts et limites restent attachés à chaque formulation.

## A. Homologie persistante H1

### A1. ODV-AEON / TTF / LCT

**Source :** [README ODV-AEON](https://github.com/jonathansearch/RATISS-ODV-AEON), [calcul TTF](https://github.com/jonathansearch/RATISS-ODV-AEON/blob/main/kernel/ttf/ttf_compute.py), [loi LCT](https://github.com/jonathansearch/RATISS-ODV-AEON/blob/main/kernel/ttf/lct_law.py).

```text
G_TTF = graphe de voisins construit sur les coordonnées
K_TTF(λ,r) = VR_r(X_λ)
L₁^max(K_TTF) = plus longue durée H1 finie
```

Dans le code LCT consulté, le paramètre source `C=|cos(θ)|` règle le quantile de compression `q=0,5C`; les points conservés alimentent le complexe de Rips. Dans la traduction de cette seule source, `λ_coh` sert d’étiquette locale pour ce paramètre; l’échelle générique du dictionnaire reste `λ`, et la dépendance `X_(q(λ_coh))` demeure explicite.

| Formulation source | Traduction canonique | Statut/source |
|---|---|---|
| `P_sig = persistance du cycle H1 fini le plus long` | `L₁^max(K_TTF)` | définition opératoire du code ciblé |
| `R = P_sig` (formulation finale) | `R_LCT := L₁^max(K_TTF)` | formulation finale README/code; l’en-tête du module conserve une ancienne formule |
| `R = P_sig/(P_noise+ε)` | `R_old := L₁^max / (N₁^TTF+ε)` | candidat historique déclaré non monotone, non retenu |
| `P_sig` croît avec `C` | `λ_coh ↑ ⇒ L₁^max(K_(q(λ_coh)))` ne décroît pas | hypothèse LCT rapportée; le filtrage dépend lui-même de `λ_coh` |
| invariance sous changement d’énergie mesurée | à forme, `θ` et pipeline fixés : `E₁≠E₂`, `L₁^max(K₁)=L₁^max(K₂)` | claim/protocole LCT; dans le test de code, `t,J` alimentent l’énergie mais ne sont pas des entrées directes du calcul H1 |
| `ΔW=η·φ·P_sig·C` | `ΔW=η·φ·L₁^max·λ_coh` | traduction des variables source, pas une nouvelle règle |

Le README rapporte des essais sur protéines, tomographie quantique et QPU; ces affirmations demeurent **rapportées par le dépôt** ici. L’indépendance d’énergie doit être lue selon le test précis, pas comme preuve universelle.

### A2. RATISS Photoinduced Topology — SSH / `Travaux`

**Sources :** [README](https://github.com/jonathansearch/Travaux), [extracteur H1](https://github.com/jonathansearch/Travaux/blob/main/ratiss_photoinduced/topology.py), [score robuste](https://github.com/jonathansearch/Travaux/blob/main/ratiss_photoinduced/robust_metrics.py).

```text
c_i = (|C_i1|,…,|C_iN|)              profil de corrélation du site i
D_ij = ||c_i − c_j||₂                distance entre profils
K_SSH = VR(D)                        complexe filtré sur ces profils
P_sig_source = L₁^max(K_SSH)         durée H1 finie maximale
```

Le score de décision combiné est traduit séparément :

```text
Edge_source = |C_(0,N−1)|           → e_boundary (corrélation de bord)
Gap_source                            → g_spectral (écart spectral)
Entropy_source                        → h_corr (entropie de corrélation)
Score_robust = L₁^max_seuil + e_boundary − 0,1 h_corr
```

`e_boundary`, `g_spectral` et `h_corr` ne sont pas des classes d’homologie. Le score robuste mélange une signature H1 et des observables distinctes.

La source rapporte, pour le modèle SSH, `L₁^max=0` du côté trivial et une valeur non nulle du côté topologique; elle rapporte aussi un contraste couplé sur QPU et l’inversion de `P_sig` seul sous certains bruits. Ce sont les résultats déclarés dans le dépôt, avec son périmètre de modèle/essai.

### A3. LeWM — plugin sur embeddings latents

**Sources :** [README d’intégration](https://github.com/jonathansearch/ratiss-lewm-integration), [`ratiss_topo_plugin.py`](https://github.com/jonathansearch/ratiss-lewm-integration/blob/main/ratiss_lewm/ratiss_topo_plugin.py).

```text
Z_b = nuage latent de la séquence b, limité à max_points
L₁^max(VR(Z_b)) = résumé H1 de cette séquence
score_plugin = moyenne_b L₁^max(VR(Z_b))
```

Le plugin utilise `ripser` lorsqu’il est disponible; sans backend, le code renvoie zéro et un statut `fallback`. Son champ source `betti_h1` compte les intervalles H1 finis retournés (`N_{1,fin}^{bars}`), pas nécessairement `β₁(K^λ)` à un seuil fixé. Le terme de perte est détaché et désactivé par défaut : la mesure est un diagnostic, pas une perte topologique différentiable intégrée au modèle.

### A4. `metac-bot-template` — topologie sémantique réelle

**Source :** [`topology_real.py`](https://github.com/jonathansearch/metac-bot-template/blob/main/ratiss_brain/topology_real.py).

```text
Z = nuage d’embeddings normalisé L₂
K = VR(Z) réduit sur F₂, H1
score_interne = L₁^sum(K) = Σ_j(d_j−b_j)
```

Ici, la réduction est la **somme** des durées H1, non leur maximum. Le score est interne au moteur de prévision; le code prévoit des statuts `disabled`, `error` et `ok`. Ce type n’est pas fusionné avec `L₁^max`.

### A5. Topological Decoherence Studio Cloud

**Sources :** [README](https://github.com/jonathansearch/ratiss-topological-decoherence-engine), [guide algorithmique](https://github.com/jonathansearch/ratiss-topological-decoherence-engine/blob/main/docs/ALGORITHM_GUIDE.md).

Pour la voie de simulation à matrice densité :

```text
M[k,i,j] = min(1, I(ρ_ij)/2)     tranche des relations à l’étape k
K_graph[k] → VR → H₀,H₁ → L₁^max(K_graph[k])
```

La langue sépare quatre sorties : `L₁^max(K_graph)`, les nombres de Betti, `S_logical(t)` du noyau de qubit logique logiciel, et `Path_G(…)` de la route TSP. Le Studio déclare explicitement que `topology.psig` et `logical_topology.P_sig` ne sont pas le même champ. Les imports de comptages QPU donnent des associations classiques, pas une inférence d’intrication.

### A6. FOCAL — conteneur H1/H2 et focalisation

**Sources :** [spécification EXP-FOCAL-01](https://github.com/jonathansearch/ratiss-focal/blob/main/SPEC-EXP-FOCAL-01.md), [formalisation](https://github.com/jonathansearch/ratiss-focal/blob/main/FORMALISATION.tex), [glossaire](https://github.com/jonathansearch/ratiss-focal/blob/main/GLOSSAIRE.md).

```text
X_F = nuage de points
K_F(ε) = VR_ε(X_F)
H₁(K_F), H₂(K_F) = classes suivies dans le conteneur
```

Dans la spécification, le conteneur est « fond + nuage + filtration VR »; H1/H2 sont suivis. `P_ref` est une ligne de base. Le scalaire appelé `P_sig` n’a pas une seule réduction explicitée dans toutes les versions/tests : écrire `L₁^max` seulement lorsqu’un protocole donne bien cette réduction; sinon garder `S_topo^{?}` et marquer la méthode ouverte.

Focalisation source :

```text
Φ(X) = (N_int × τ) / V_info
Φ(X) ≥ Φ_c(X)  →  focalisation déclarée
```

Langue RATISS : `λ_conc(X) ≥ λ_c(X) → onset_focal(X)`. La source ne fixe pas systématiquement le degré `k` ni le critère `β_k>0`; on ne les ajoute pas par défaut.

### A7. VRN — neurone topologique exploratoire

**Sources :** [README VRN](https://github.com/jonathansearch/ratiss-vrn), [SPEC-V0](https://github.com/jonathansearch/ratiss-vrn/blob/main/SPEC-V0.md).

```text
s = JEPA(x)
P_sig(s) = persistance H1 annoncée
g = Γ(P_sig(s))              Γ/seuil/fonction : ouverts
y = g · (s ⊕ concept(s))    fusion : ouverte
```

Langue RATISS : `s=Embed(x)`, puis `g=Gate(L₁^max(K_latent(s)))` **si** le plugin H1-max est choisi. `Gate` et l’opération de fusion du signal/concept demeurent des décisions ouvertes dans la spécification. Statut : exploration/spécification, pas résultat conclu.

### A8. RATISS-Bio — signature biomoléculaire H1/H2

**Sources :** [README](https://github.com/jonathansearch/ratiss-bio), [`bio114/topology.py`](https://github.com/jonathansearch/ratiss-bio/blob/main/bio114/topology.py).

La chaîne source devient un nuage 3D; la routine de persistance construit Vietoris–Rips jusqu’à H2, seuil `30 Å`, avec sous-échantillonnage à 220 points. Pour les barres finies de longueur supérieure à `1 Å`, le code somme séparément les degrés 1 et 2, puis calcule :

```text
T_k = Σ_(j : ℓ_j^k > 1 Å) ℓ_j^k
S_bio = 1 − exp(−(T₁ + 1,5·T₂)/(15·max(1,N)))
```

`S_bio` est donc un agrégat pondéré H1/H2, pas la plus longue barre H1. Le module compare aussi deux fiches par :

```text
d_sig(a,b) = |S_bio(a)−S_bio(b)|
           + 0,05·|n₁(a)−n₁(b)|/max(1,n₁(a)+n₁(b))
           + 0,05·|n₂(a)−n₂(b)|/max(1,n₂(a)+n₂(b))
```

`d_sig` est une distance composite entre fiches, pas une nouvelle persistance. Le README décrit aussi des protéines en nuages Cα; le module contient un constructeur de géométrie d’ADN. La source d’entrée et le pipeline doivent être précisés expérience par expérience. L’observable `Xi_IDP = ⟨H1⟩_ensemble/S_conf` est rapportée pour le désordre fonctionnel, mais le degré/agrégateur de `H1` doit être lié au calcul utilisé avant toute comparaison. PIP2 anchoring et comptes de boucles restent des champs d’observation distincts. Le dépôt décrit des résultats *in silico*; la notation ne change pas leur statut.

### A9. RATISS-NEURO — signature temporelle et plasticité homologique

**Sources :** [`topology.py`](https://github.com/jonathansearch/ratiss-neuro/blob/main/ratiss_neuro/topology.py), [`topo_plasticity.py`](https://github.com/jonathansearch/ratiss-neuro/blob/main/ratiss_neuro/topo_plasticity.py), [README](https://github.com/jonathansearch/ratiss-neuro).

Pour chaque fenêtre du signal EEG/spike, le code standardise le segment, construit un embedding de Takens (`dim=3`, `delay=8` échantillons), calcule une filtration Vietoris–Rips et réduit les longueurs H1 finies en `S_neuro(w)∈[0,1]` (définition détaillée dans [03 — Signatures](03_SIGNATURES.md)). La série `P_sig^neuro(t)` est le score des fenêtres; le pic, la durée moyenne H1 convertie en ms et le nombre de barres H2 sont des sorties séparées. La persistance H2 est calculée seulement pour les nuages suffisamment petits selon le code.

Le module `topo_plasticity.py` prend un échantillon de neurones sentinelles, applique à leurs corrélations cosinus le seuil médian des valeurs positives, puis emploie Kruskal/union-find. Les arêtes hors arbre forment un masque de synapses et leur nombre est un proxy de cycles du **graphe seuillé**. Dans la langue, c’est un rang cyclomatique d’un graphe de dimension 1; ce n’est pas le même calcul que la persistance H1 sur un complexe de Vietoris–Rips.

Le module `topology.py` définit aussi `graph_sublevel_persistence(f, G)`: filtration sous-niveau du champ `|ψ|²` sur un graphe d’adjacence, suivi du plus grand intervalle fini H0 et normalisation par `max(f)−min(f)+10⁻¹²`. Traduction : `S_sub0(f,G)=clip(L₀^max(K_f)/range(f),0,1)`. Cette signature H0 de graphe est distincte du score H1 du plongement Takens.

### A10. RATISS Aeon Prime — risque sur surface d’attaque

**Source :** [README, module de scan défensif](https://github.com/jonathansearch/ratiss-aeon-agent).

Le README annonce l’application de `β₀, β₁, β₂` à une surface d’attaque; `β₁` doit repérer des cycles interprétés comme « kill chains », puis un score topologique de risque entre 0 et 100. Traduction : `K_attack` (construction à citer), `β_k(K_attack)` si le complexe est effectivement spécifié, puis `S_risk^topo` comme score aval. La construction du complexe, la filtration, le réducteur et la fonction de conversion 0–100 ne sont pas donnés dans le README consulté : le score reste `S_topo^{?}`, non comparable et non reconstructible à partir du seul nom « Betti ».

### A11. Réseaux corrélationnels et décisions aval

**Sources :** [`Crypto-net-veo-/ratiss_topo/topology.py`](https://github.com/jonathansearch/Crypto-net-veo-/blob/main/ratiss_topo/topology.py), [arsenal cyber](https://github.com/jonathansearch/Crypto-net-veo-/blob/main/ratiss_topo/arsenal.py), [`ratiss-Skynet` score](https://github.com/jonathansearch/ratiss-Skynet/blob/main/ratiss_skynet/skynet/topo_score.py), [`RATISS-Jonathan-Labs`](https://github.com/jonathansearch/Ratiss-Jonathan-Labs-).

Les calculs VR partagent ici un réducteur de type `L₁^max`, mais pas le même espace métrique :

```text
Cyber : profils_i = |C_i,:| ; D_ij = ||profils_i − profils_j||₂ ; P_sig = L₁^max(VR(D))
Skynet : D = 1 − corr(activations) ; P_sig = L₁^max(VR(D))
Jonathan-Labs : P_sig de l’association/affinité, Betti et route d’inspection exportés séparément
```

Dans les copies du moteur cyber/Skynet, les simplexes de Rips sont construits jusqu’en dimension 2 sur `F₂`, avec coupure `max_edge`; `P_sig` est le maximum des durées H1 finies supérieures à `10⁻⁹`. Les classes encore non appariées à la coupure ne font pas partie de ce maximum, tandis que le champ `betti` rapporte les classes survivantes. Le seuil doit accompagner toute comparaison.

Le cyber dispose aussi de canaux non homologiques :

```text
z_t = max(0, (a_t − μ_ref)/σ_ref)
h_t = exp(−1/τ_h)·h_(t−1) + (1−exp(−1/τ_h))·z_t
D_t = ||C_t − C_ref||_F
f_tri = #{i<j<k : C_ij·C_jk·C_ik < −10⁻⁹} / max(1, binom(d,3))
```

`h_t` est la trace d’hystérésis, `D_t` l’écart au profil de corrélation de référence, et `f_tri` la fraction de triangles frustrés. Dans le code Kibble–Zurek consulté, le champ nommé `cumul_drift` vaut `D_t` (écart courant), et non une somme temporelle; `gel` est un rapport moyenne/écart-type des `D_t` récents. Ce sont des métriques de dynamique et de motifs de graphe, pas des Betti.

Dans RATISS-Fusion-stark, `confiance_certifiée = confiance_needle × P_sig` est une règle de fusion/filtrage aval. Elle n’est pas une nouvelle définition de persistance ni une preuve que la réponse est vraie. Le solveur AEON/Fusion avec GUDHI somme les longueurs H1, en remplaçant chaque décès infini par `1,5·max_edge` avant la somme :

```text
S_H1^GUDHI = Σ_j (d'_j − b_j),   d'_j = d_j si fini, sinon 1,5·max_edge
β₁^fallback = max(1, int(# {e : longueur(e) < 0,4·max_edge}/(N+1)))
```

Le fallback natif n’effectue pas une réduction persistante H1 et, sans diagramme H1, le code retourne `S_H1=0,5`. Les deux chemins doivent être identifiés dans tout résultat et ne sont pas interchangeables.

## B. Géométrie de trajectoire : RATISS-GRID

**Sources :** [code `topology.py`](https://github.com/jonathansearch/RATISS-GRID/blob/main/ratiss_grid/topology.py), [mémo d’état](https://github.com/jonathansearch/RATISS-GRID/blob/main/MEMO_GRID.md).

```text
Z_τ(s) = Delay_τ(s) = {(s_i,s_(i+τ))}
A_τ^norm(s) = |aire shoelace(Z_τ(s))| / (n Var(s)+ε)
r_santé = A_τ^norm(fenêtre) / A_τ^norm(référence saine)
healthy ⇔ r_santé > 0,5
```

Le premier passage de `update` fixe la référence saine. Le seuil `0,5` est un seuil logiciel de surveillance, pas une loi topologique universelle. Le mémo indique que cette aire est validée sur signaux synthétiques et que le pouvoir prédictif terrain exige des mesures du prototype.

**Écart source à conserver :** le README parle de H1/Vietoris–Rips; le code et le mémo donnent l’aire Takens comme mesure réellement implémentée, et le mémo dit explicitement « PAS H1 Vietoris–Rips ». Dans le dictionnaire, l’implémentation est `A_τ^norm`, et l’écart documentaire reste visible.

## C. Boucles, graphes et structures d’activation

### C1. RATISS-X et banc Mixer

**Sources :** [hypothèses/specification RATISS-X locale](../../uploads/RATISS_X_HYPOTHESES_ET_ARCHITECTURE_FONDATRICE.md), [banc d’essai local](../../banc_essai_mixer/moteur_topologique.py).

Le document de spécification pose un seuillage d’activations et un graphe d’activation :

```text
V_l^ε = { i : |a_i^(l)| > ε }
G_l^ε = (V_l^ε, E_l)       E_l n’est pas défini complètement dans la spécification
```

Le banc Mixer construit par couche des ensembles `A_l(x)` contenant les 5 % d’unités les plus actives, puis compare deux questions :

```text
J_l(x,y) = |A_l(x)∩A_l(y)| / |A_l(x)∪A_l(y)|
J_route(x,y) = moyenne_l J_l(x,y)
```

C’est un recouvrement d’ensembles actifs par couche, pas un calcul H1. « Cheminée »/« route stationnaire » reste le nom de projet; la règle de construction des arêtes n’est pas entièrement spécifiée par ce banc.

### C2. RATISS-ONE / tissu Ratum

**Source :** [spécification Ratum v3](https://github.com/jonathansearch/RATISS-ONE/blob/main/ratum/LANGAGE-RATUM.md).

```text
G_tissu = (V, E_assoc^non-dir, E_seq^dir)
```

Le tissu associe via des liens non orientés; la bouche encode une succession dirigée. La charge du neurone est transitoire, la force du lien persiste. C’est une **topologie de réseau typée**; aucune homologie H1/H2 n’est inférée tant qu’un complexe et une filtration ne sont pas construits.

## D. Formulations transversales et géométriques

### D1. FOCAL — liens entre couches

La source emploie `P_sig(X↔Y)` pour le phase-locking entre couches. Traduction :

```text
Γ_XY^phase(t)        relation temporelle de phase entre couches
Sync(…)              mesure d’accord, selon la formule propre au test
```

Dans `FORMALISATION.tex`, `Ψ_sync=(f₁f₂f₃)^(1/3)` pour un test donné. D’autres documents donnent d’autres constructions de sync; le dictionnaire ne les identifie pas sans préciser la version.

Les autres expressions proches de la topologie sont gardées comme **descripteurs inter-couches**, pas comme homologie :

| Source | Sens canonique RATISS |
|---|---|
| `X=(1/3)Σ_(i<j)abs(corr(P_i,P_j))` | `CrossCorr(layers)` — corrélation inter-couches |
| `U=P_joint−Σ_iP_i` | `JointExcess` — excès/écart de mesure conjointe, selon le protocole |
| `I(X→Y)` | `Influence(X→Y)` — quantité dirigée source; deux formules source coexistent (glossaire et formalisation) |
| `K(L)=1−P_L/P_joint` | `κ_sep(L)` — séparateur global/individuel, pas un complexe |
| `Φ(X)≥Φ_c(X)` | `λ_conc(X)≥λ_c(X)` — seuil de concentration/focalisation |

Pour `I(X→Y)`, le glossaire donne `ΔP_sig^Y/A^X`; la formalisation donne `(P_(Y+pont)−P_Y−P_pont)/A^X`. Le dictionnaire les conserve comme deux versions source d’`Influence(X→Y)` jusqu’à harmonisation; ce terme décrit une relation dirigée, pas une classe d’homologie.

### D2. CONTINUUMS

**Source :** [PROTOCOLES C01–C09](https://github.com/jonathansearch/ratiss-continuums/blob/main/PROTOCOLES.md). Les lignes ci-dessous traduisent les structures, sans valider les lois rapportées.

| Test | Formulation source | Langue du dictionnaire / type |
|---|---|---|
| C01 — Berry | boucle fermée; phase par qubit `γ=−φ/2`; frange seulement dans les corrélations dans le résultat rapporté | `Hol_γ` sur boucle de paramètres; géométrie de phase, distincte de H1 persistant |
| C04 — twist | réseau anneau+hubs; pour N puits symétriques, twist rapporté nul dès N≥3 | `Tw_model(N,sym)` observable de torsion du modèle; formule de construction à rattacher au code |
| C05 — focalisation | `P_sig` croît avec N condensateurs, rendements décroissants | `S_topo(N)` croissant selon le protocole; réduction exacte du `P_sig` à préciser avant comparaison |
| C07 — G à N corps | `G(N)=mean_(200 derniers pas)(p_sig/P_REF)`; diminution sous couplage, valeur nulle au réglage le plus fort, appelée « mort topologique » dans la source | `S_norm(c,N)` signal normalisé; ne pas l’identifier à `β₁=0` sans diagrammes/code correspondant |
| C09 — seuil fini | Kuramoto : plat loin du régime critique, éventail/crossover proche du régime critique, sans `N_c` franc | dynamique de synchronisation à taille finie; pas un invariant homologique |

C02 (loi d’échelle de décohérence), C03 (factorisation), C06 (mémoire) et C08 (Ramsey/écho) sont des lois temporelles/physiques rapportées. Elles peuvent être attachées à un complexe ou une application dans une étude ultérieure; elles ne deviennent pas topologiques par simple renommage.

## E. Géométrie, gravitation et signatures de phase

### E1. `synchrotron-24` — nuages de positions, mémoire et confinement

**Sources :** [`organes/conteneur.py`](https://github.com/jonathansearch/synchrotron-24/blob/main/organes/conteneur.py), [`S03`](https://github.com/jonathansearch/synchrotron-24/blob/main/experiences/s03_rebond.py), [`S05`](https://github.com/jonathansearch/synchrotron-24/blob/main/experiences/s05_fantome.py), [protocoles](https://github.com/jonathansearch/synchrotron-24/blob/main/PROTOCOLES.md), [lois](https://github.com/jonathansearch/synchrotron-24/blob/main/LOIS.md).

Deux calculs source distincts coexistent :

```text
H1_S03/S05(t) = L₁^max(VR(X_t))        # plus longue barre H1 finie sur les positions
P_sig_conteneur(X) = Σ_(k=1,2) Σ_(j : ℓ_j^k > 0,05) ℓ_j^k
```

S03/S05 appellent `H1` une **durée** de persistance, pas un Betti. Le conteneur, lui, additionne les durées H1 et H2 au-dessus de `0,05`. Le rapport source `H1/r≈0,178` est un ratio d’échelle calculé dans un scénario particulier, non un invariant universel; les unités et la normalisation doivent rester attachées au protocole.

S06b formule une condition de fermeture pour le champ de messagers : tore périodique (source : `H1≠0`, traduit comme `β₁(K_tore)>0`) et critère d’enroulement de trajectoire `|Δθ|>π`. Le premier est une condition homologique du domaine modélisé; le second est un seuil dynamique de winding. Ils ne sont pas interchangeables. L’affirmation source « gravité véhiculée exige la fermeture » et le transfert de H1 vers des orbiteurs sont des résultats rapportés du modèle; faute d’application induite `f_*` et d’un protocole de preuve indépendant, le dictionnaire n’en déduit pas un transfert physique démontré.

### E2. `scientist-research` — gradient topologique en gravitation

**Sources :** [README](https://github.com/jonathansearch/scientist-research-), [formulation historique `P_sig`](https://github.com/jonathansearch/Porte-folio-Jonathan-).

La source affiche les formulations suivantes :

```text
Λ_LCT ∝ ∇P_sig
G_(μν) + Λ_(LCT,μν) = 8πG · T^eff_(μν)
```

pour la stabilisation d’une paroi de bulle; dans cette formule source, `G_(μν)` est le tenseur d’Einstein, non le graphe `G_D`. Dans la langue du dictionnaire, on écrit provisoirement `S_topo` pour la signature utilisée et `∇S_topo` pour sa variation spatiale; on ne lui attribue le type `L₁^max` que si le diagramme, la filtration et les unités sont ceux du calcul H1-max identifié. La définition tensorielle, les unités, le domaine de dérivation et le passage de scalaire à tenseur restent **ouverts**. C’est une hypothèse de couplage rapportée, pas une loi physique validée par la notation. Le README source rapporte lui-même que deux formulations testées ont échoué et que le tenseur 4D complet n’est pas établi.

### E3. RATISS-PHOTON — hypothèse de tension et vortex de phase

**Sources :** [spécification physique](https://github.com/jonathansearch/RATISS-PHOTON/blob/main/spec_physics.md), [campagne](https://github.com/jonathansearch/RATISS-PHOTON/blob/main/experiences/campagne.py).

L’hypothèse `H1` du dépôt — probabilité comme support/tension topologique — est conceptuelle et n’a pas de définition d’espace, complexe ou invariant. L’observable opérationnelle `O2` est le comptage de vortex de phase `N_vort^{gate}` : winding de `arg(ψ)` égal à `±2π` autour d’une plaquette, avec filtre d’amplitude. Ce comptage est un défaut de phase local, distinct de H1 persistant. Le dépôt précise que ses résultats portent sur un simulateur et ne prouvent pas la nature de photons réels.

## F. États quantiques, graphes QPU et sidecars logiciels

### F1. QPU-Ratiss-COSMOS — trois flux qu’il ne faut pas fusionner

**Source :** [README COSMOS](https://github.com/jonathansearch/QPU-Ratiss-COSMOS).

Le contrat distingue (i) `P_sig` du graphe d’associations tiré des comptages, (ii) `logical P_sig` de la trajectoire de densité traitée par le sidecar logiciel, et (iii) la tension du canal d’incubation `Ψ=Q×I×M`. Le graphe peut valoir zéro sans être remplacé par le sidecar; le `P_sig` logique n’est pas reconstruit depuis les seuls comptages. La méthode générale indique Vietoris–Rips GF(2) et H0/H1, mais le réducteur précis du champ `P_sig` doit être lié au contrat/version d’artefact : on le garde `S_graph^{?}` en attendant. `Ψ` est un produit de canal, pas un invariant topologique.

### F2. Banc Grover et RATISS Quantum Topology Studio

**Sources :** [banc Grover](https://github.com/jonathansearch/Algorithmes-quantique-Ratiss-labs-), [Studio personnel](https://github.com/jonathansearch/ratiss-decoherence-atlas), [guide du moteur](https://github.com/jonathansearch/ratiss-topological-decoherence-engine/blob/main/docs/ALGORITHM_GUIDE.md).

Le banc Grover suit un `TopologicalQubit` logiciel en flux séparé; son `P_sig` n’est pas calculé à partir de la masse de l’état Grover. Le champ de comptages d’association est encore un autre objet. Le moteur a documenté un correctif de tolérance `10⁻⁹` pour ne plus compter comme persistants des cycles dégénérés de longueur numérique quasi nulle. Dans le Studio, le graphe, le qubit logique, la phase, le twist, la protection et la route TSP sont des champs distincts; les dessins rejouent les valeurs exportées et ne constituent ni mesure matérielle ni preuve de correction d’erreur.

### F3. QPU-AMBIENT — rayon de Bloch, pas homologie

**Source :** [`coherence.py`](https://github.com/jonathansearch/RATISS-QPU-AMBIENT/blob/main/ratiss_qpu/coherence.py).

La trajectoire de vecteur de Bloch `r⃗(t)` produit `S_Bloch = moyenne_t ||r⃗(t)||`. Le code le décrit comme contraction radiale associée à la pureté/cohérence. Cela mesure une position géométrique dans la sphère de Bloch, sans complexe filtré ni diagramme de persistance; `P_sig` est ici un alias source, pas un invariant homologique.

## G. Formulations voisines qui restent hors du noyau homologique

| Corpus | Formulation existante | Classe dans le dictionnaire |
|---|---|---|
| RATISS-SIMULTANEITE | CHSH, identité de Kuramoto, verrouillage à un forçage | mesure de corrélation/synchronisation; aucune homologie par défaut |
| RATISS-GTT | conservation, déterminant symplectique, aller-retour réversible | invariants algébriques/dynamiques; une application peut en plus induire une action sur `H_k` |
| RATISS-PLANCK | échelles de Planck, limites de mesure, formules dimensionnelles | physique théorique; pas de complexe/topologie explicite dans les éléments consultés |
| RATISS-NEURALINK-POC | classes discrètes `winding_class` de micro-cycles | sortie catégorielle/dynamique; à typer par son calcul avant de l’appeler invariant de winding |
| chemins, routes TSP, score de risque Aeon Prime | graphe de chemins, inspection ou décision aval | objets distincts; Hk seulement si la construction complexe est déclarée |

Leur classement hors de l’homologie n’est pas un rejet de ces travaux : il évite d’appeler « persistance » une quantité de phase, de graphe ou de décision qui n’a pas été définie par un diagramme de persistance.