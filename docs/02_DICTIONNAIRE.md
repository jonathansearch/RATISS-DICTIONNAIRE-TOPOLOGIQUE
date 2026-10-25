# 02 — Dictionnaire des symboles

Le sens de gauche est celui du dictionnaire RATISS. Les signes peuvent exister ailleurs en mathématiques avec d’autres usages : **l’indice, l’objet et le contexte font partie du symbole**.

## Objets et relations

| Symbole | Définition canonique | Rôle dans un travail RATISS |
|---|---|---|
| `D` | étiquette d’un domaine | quantique, géométrique, thermodynamique, informationnel, réseau, latent, etc. |
| `V_D` | ensemble d’objets du domaine | qubits, régions, sites, états, nœuds d’un graphe, points d’un nuage |
| `E_D^r` | relations binaires de type `r` | `assoc` association; `seq` succession dirigée; `phase` relation de phase; `meas` relation mesurée |
| `G_D^r=(V_D,E_D^r)` | graphe typé | réseau à liens orientés/non orientés, pondérés ou non |
| `K_D=(V_D,Σ_D)` | complexe simplicial | réseau avec relations d’ordre supérieur; `Σ_D` contient les simplexes et leurs faces |
| `X_D` | espace ou nuage muni d’une distance/topologie | trajectoire, embedding, coordonnées, configurations géométriques |
| `Cl(S)` | fermeture simpliciale de `S` | complète les faces nécessaires après ajout de relations |
| `Γ_AB^r` | relation inter-domaines de type `r` | pont entre éléments de A et B; `r` distingue analogie, représentation, phase ou observation |
| `K_(A⋈B)` | `Cl(K_A ⊔ K_B ∪ Γ_AB^r)` | assemblage topologique des couches A et B |
| `f_AB` | application structurelle `K_A→K_B` | représentation/traduction déterminée; pas une causalité par défaut |
| `f_AB*` | application induite `H_k(K_A)→H_k(K_B)` | classes topologiques de A qui ont une image dans B |

## Cycles, trous et invariants

| Symbole | Définition canonique | Lecture |
|---|---|---|
| `Ch_k(K)` | groupe des chaînes de dimension k | combinaisons de simplexes de dimension k |
| `∂_k` | application de bord | envoie une chaîne vers son bord; `∂_(k−1)∂_k=0` |
| `Z_k(K)=ker ∂_k` | cycles | chaînes sans bord |
| `B_k(K)=im ∂_(k+1)` | bords | cycles remplissables par une chaîne de dimension k+1 |
| `H_k(K)=Z_k/B_k` | homologie de degré k | cycles considérés à équivalence près par remplissage |
| `β_k(K)=rank H_k(K)` | nombre de Betti | nombre de classes indépendantes au degré k |
| `β_k(K^λ)` | nombre de Betti au niveau `λ` | classes présentes à cette échelle précise de la filtration |
| `χ(K)=Σ_k(−1)^kβ_k(K)` | caractéristique d’Euler | résumé alterné des nombres de Betti |
| `H_0`, `H_1`, `H_2` | degrés topologiques | composantes, boucles, cavités/enveloppes, dans le modèle construit |
| `im(f_AB*)` | image sur l’homologie | classes qui sont représentées après le passage A→B |
| `ker(f_AB*)` | noyau sur l’homologie | classes de A effacées par l’application au degré étudié |
| `H_k(K_A)≅H_k(K_B)` | isomorphisme au degré k | mêmes groupes d’homologie en ce degré; pas identité des systèmes physiques |

> Dans ce dictionnaire, `Ch_k` désigne le groupe des chaînes; il n’est pas le `C` de cohérence des sources LCT.

## Distance, échelle et durée

| Symbole | Définition canonique | Usage |
|---|---|---|
| `VR_ε(X)` | complexe de Vietoris–Rips au rayon `ε` | transforme une géométrie métrique en complexe; `ε` est l’échelle |
| `K^λ` | complexe construit au niveau du paramètre `λ` | filtration par distance, seuil, bruit, temps, couplage ou autre variable étiquetée |
| `𝒟_k(K^λ)` | diagramme de persistance de degré k | ensemble des intervalles de naissance/disparition |
| `N_{k,fin}^{bars}` | nombre d’intervalles finis au degré k | à distinguer de `β_k(K^λ)`, nombre de classes présentes à un niveau fixé |
| `I_j^k=[b_j,d_j)` | intervalle de persistance j | classe présente entre les niveaux `b_j` et `d_j` |
| `ℓ_j^k=d_j−b_j` | durée de l’intervalle j | persistance en unité de `λ` |
| `L_k^max(K)=max_(j∈I_{k,fin}) ℓ_j^k` | durée maximale finie | plus longue classe finie au degré k |
| `L_k^sum(K)=Σ_(j∈I_{k,fin})ℓ_j^k` | persistance totale finie | somme des durées finies au degré k |
| `L_{1,2}^{sum,>δ}(K)` | `Σ_(k=1,2)Σ_(j:ℓ_j^k>δ)ℓ_j^k` | somme multi-degrés à seuil explicite, sans normalisation sauf mention |
| `T_k^{>δ}` | `Σ_(j:ℓ_j^k>δ)ℓ_j^k` | persistance totale finie du degré k au-dessus du seuil `δ` |
| `Δ_Γβ_k` | `β_k(K_(A⋈B))−β_k(K_A⊔K_B)` | changement net du nombre de classes k après ajout des liens `Γ` |
| `λ_c` | seuil déclaré | niveau de transition; sa signification dépend du domaine |

Les intervalles infinis ne sont pas inclus dans `L_k^max` ou `L_k^sum` sans convention écrite.

## Trajectoires et phase

| Symbole | Définition canonique | Nature |
|---|---|---|
| `Delay_τ(s)` | nuage ` {(s_i,s_(i+τ))} ` | plongement retardé d’un signal scalaire en dimension 2 |
| `A_τ^norm(s)` | aire absolue du cycle retardé, normalisée par fenêtre et variance | signature géométrique de trajectoire; **pas** une homologie persistante |
| `Hol_γ` | phase accumulée le long d’un chemin fermé `γ` | holonomie/phase géométrique; distincte de la durée d’un cycle H1 |
| `Path_G(u,v)` | ensemble des chemins reliant `u` à `v` dans `G` | routes du réseau, non invariant de persistance par défaut |
| `Sync(D₁,…,D_n)` | valeur d’accord entre couches | descripteur de synchronisation; sa formule est propre au protocole |
| `Γ_AB^phase(t)` | relation de phase entre couches A et B au temps t | type de relation; n’est pas une classe H1 sans construction supplémentaire |
| `g_topo` | sortie d’une règle de décision alimentée par une signature topologique | porte/gate; sa fonction (seuil, sigmoïde…) doit être spécifiée |

## Indicateurs spécifiques et mesures voisines

| Symbole du dictionnaire | Construction ou définition | Distinction à conserver |
|---|---|---|
| `S_bio` | `1−exp(−(T₁^{>1Å}+1,5·T₂^{>1Å})/(15·max(1,N)))` | agrégat biomoléculaire H1/H2; ne vaut pas `L₁^max` |
| `S_neuro(w)` | score H1 normalisé d’une fenêtre Takens; voir [03 — Signatures](03_SIGNATURES.md) | série temporelle; durées H1 en ms et comptes H2 restent des champs séparés |
| `S_sub0(f,G)` | persistance H0 maximale d’une filtration sous-niveau du champ `f` sur le graphe `G`, divisée par l’étendue de `f` | score borné du module neuro; différent de H1 sur le nuage de Takens |
| `S_Bloch` | moyenne de `‖r⃗(t_i)‖` sur une trajectoire | rayon de Bloch / cohérence géométrique; pas d’homologie persistante |
| `N_vort^{gate}` | compte des plaquettes à winding de phase `±2π` après gate d’amplitude | vortex locaux; pas un `β₁` ni un compte de barres H1 |
| `S_logical(t)` | sortie du sidecar logiciel de qubit logique | pas la signature du graphe ni une mesure physique par défaut |
| `S_graph^{?}` | signature annoncée sur graphe d’associations de comptages QPU | réducteur/méthode à citer par version; ne pas remplacer par `S_logical` |
| `S_risk^{topo}` | score aval de risque annoncé sur une surface d’attaque | formule et conversion à définir dans la source avant comparaison |
| `Xi_IDP` | `⟨H₁⟩_ensemble/S_conf` dans RATISS-Bio | garder la définition de `H₁` et l’entropie conformationnelle propres au protocole |
| `Ψ_sync` | score d’accord entre composantes selon le test source | mesure de synchronisation; pas un invariant homologique |

## Noms de sources non canoniques

| Nom source | Règle du dictionnaire |
|---|---|
| `P_sig`, `p_sig` | alias historique à convertir selon le calcul réel; jamais comparé sans indice de méthode |
| `C` | symbole source (cohérence, corrélation, chaîne… selon dépôt); ne pas réutiliser sans indice |
| `R` | réponse, ratio ou score selon la source; toujours qualifier `R` par méthode et domaine |
| `Φ`, `Φ_c` | concentration/seuil dans FOCAL; le dictionnaire emploie `λ_conc`, `λ_c` lorsqu’il s’agit d’une échelle |
| `Γ` sans indices dans VRN | fonction de gate exploratoire; dans le dictionnaire, `Γ_AB^r` désigne seulement un pont relationnel |
| `K(L)` dans FOCAL | séparateur global/individuel; à renommer `κ_sep(L)` pour ne pas le confondre avec le complexe `K` |
| `H2'` dans FOCAL | étiquette d’une hypothèse; distincte de `H₂(K)`, homologie de degré 2 |
| `λ_coh` | étiquette de traduction gardée pour le paramètre source de cohérence dans une filtration LCT; pas une variable canonique de tous les domaines |
| `λ_conc` | paramètre de concentration dans les traductions des seuils FOCAL; garde le lien vers la définition source |
| `N₁^TTF` | estimateur de bruit H1 défini par le code TTF; détail dans [03 — Signatures](03_SIGNATURES.md) |
| `S_topo^{?}` | mesure source appelée topologique, mais dont le type/méthode n’est pas défini |
| `Tw_model` | observable de torsion du modèle Continuums; à ne pas assimiler à un nombre d’enroulement sans définition de calcul |
| `S_norm` | signal topologique normalisé par une référence; le sous-type dépend du protocole |

Pour les différentes traductions de `P_sig`, voir [03 — Signatures](03_SIGNATURES.md).