# 05 — Ponts entre domaines, statuts et provenance

## 1. Types de pont

| Type | Notation | Signification | Ne signifie pas |
|---|---|---|---|
| Analogie de forme | `Γ_AB^ana` | deux domaines présentent une organisation comparable | même mécanisme ou même loi |
| Représentation/traduction | `f_AB^rep : K_A→K_B` | une représentation déclarée relie A à B | causalité ou réalisation physique |
| Relation/couplage observé | `Γ_AB^obs` | interaction inscrite dans des données ou une mesure décrite | loi universelle |
| Équivalence homologique au degré k | `H_k(K_A)≅H_k(K_B)` | groupes d’homologie isomorphes pour le k choisi | identité des objets, des dynamiques ou des théories |
| Loi commune candidate | même relation quantitative avec variables et conditions appariées | possibilité de transférer une relation après mise en correspondance | universalité déjà démontrée |

Une formule porte le type de pont en indice ou dans sa fiche de provenance. Si le type n’est pas connu, écrire **pont non déterminé**.

## 2. Échelle de statut

| Statut | Sens à conserver |
|---|---|
| `IDÉE` | piste, sans prédiction testée |
| `HYPOTHÈSE` | proposition susceptible d’échouer, conditions à préciser |
| `SPÉCIFICATION` | définition/architecture écrite; pas preuve d’implémentation |
| `CODE` | implémentation repérée; pas validation automatique |
| `TEST` | protocole exécuté, avec périmètre identifiable |
| `SIMULATION` | observation dans le modèle calculé |
| `QPU` / `MATÉRIEL` | observation associée à une trace matérielle déclarée |
| `REPRODUIT` | rejoué dans des conditions indiquées |
| `CONCLUSION BORNÉE` | valable seulement dans les données/conditions rapportées |
| `OUVERT`, `MIXTE`, `RÉFUTÉ`, `NON MESURÉ` | états distincts, à ne pas convertir en succès ou échec général |

Le statut décrit le niveau d’appui, pas la nature mathématique du symbole.

## 3. Provenance minimale d’une entrée

```text
source      dépôt + fichier/section/version
objet       graphe, complexe, espace, trajectoire ou assemblage
construction distance, seuil, graphe d’arêtes, fermeture, filtrage…
mesure      L₁^max, L₁^sum, A_τ^norm, autre signature typée
pont        analogie, représentation, relation observée, loi candidate
statut      idée / hypothèse / spécification / code / test / observation…
limite       ce que la formulation ne permet pas de conclure
```

## 4. Concordances et divergences visibles dans les sources

| Point | Constat à garder visible |
|---|---|
| `P_sig` | selon la source, H1 maximal, somme H1/H2 pondérée, somme de barres, aire Takens, score neuro, rayon de Bloch, phase-lock, vortex ou sortie logique; voir [03 — Signatures](03_SIGNATURES.md) et [04 — Formulations](04_FORMULATIONS_EXISTANTES.md) |
| LCT ODV | README/code final : `R=P_sig`; l’en-tête du fichier conserve l’ancien ratio `P_sig/P_noise`, déclaré non monotone plus bas dans le code |
| GRID | README parle d’H1/VR; code et mémo identifient l’aire Takens comme l’implémentation et écartent le score H1 naïf |
| FOCAL | `P_sig`, `Φ`, `Ψ_sync`, influence et séparateur changent de rôle selon les documents; méthodes et versions doivent rester attachées |
| FOCAL — tests | les documents consultés donnent plusieurs comptages (badge 94; abstract 69+15; anciennes sections 63, et plus tard des tests 64–94); ne pas les fusionner sans audit |
| VRN | mécanisme du gate `Γ` et fusion `⊕` explicitement ouverts dans la spec v0 |
| RATISS-X | graphe des « cheminées » spécifié au niveau conceptuel; la construction de toutes les arêtes n’est pas entièrement définie par la spécification consultée |
| Continuums | les C01–C09 mélangent simulations et résultats matériels déclarés; chaque protocole précise son périmètre; les lois de synchronisation ne deviennent pas homologies par le nom « topologique » |

## 5. Couverture des sources de cette édition

| Source | Élément pris dans le dictionnaire | Statut de lecture dans cette édition |
|---|---|---|
| [RATISS-ODV-AEON](https://github.com/jonathansearch/RATISS-ODV-AEON) | graphe TTF, Rips/Betti, LCT, H1 maximal, invariant d’énergie déclaré | README + code LCT/TTF ciblé lus; mesures du dépôt non rejouées ici |
| [Travaux](https://github.com/jonathansearch/Travaux) | H1-VR, SSH, edge, gap, entropie, score robuste | README + extracteur H1/score ciblés lus; résultats conservés comme rapportés par le dépôt |
| [RATISS-GRID](https://github.com/jonathansearch/RATISS-GRID) | retard de Takens, aire, référence saine, seuil de surveillance | code + mémo consultés; validation physique explicitement en attente dans le mémo |
| [ratiss-focal](https://github.com/jonathansearch/ratiss-focal) | conteneur H1/H2, seuil de focalisation, couches, influence, séparateur | glossaire, formalisation, spécification et protocoles consultés; divergences documentaires gardées |
| [ratiss-continuums](https://github.com/jonathansearch/ratiss-continuums) | boucle de Berry, twist, signature de focalisation, érosion/crossover | protocoles C01–C09 consultés; résultats restent dans leur statut source |
| [Topological Decoherence Studio](https://github.com/jonathansearch/ratiss-topological-decoherence-engine) | relations par étape, Rips/Betti, graphe vs signature logique, routes | README + guide algorithmique consultés; pas d’audit indépendant des résultats |
| [ratiss-lewm-integration](https://github.com/jonathansearch/ratiss-lewm-integration) | durée H1 maximale sur embeddings latents | README + plugin consultés; A/B réel LeWM non établi par ces sources seules |
| [metac-bot-template](https://github.com/jonathansearch/metac-bot-template) | H1 sur embeddings; somme des durées; score interne | code `topology_real.py` consulté; pas assimilé au plugin LeWM |
| [ratiss-vrn](https://github.com/jonathansearch/ratiss-vrn) | embedding → signature → gate → concept | README + spécification v0; plusieurs fonctions ouvertes |
| [RATISS-X](https://github.com/jonathansearch/RATISS-X) et banc Mixer local | seuillage d’activations, graphe de routes, chevauchement de chemins | spécification et script local consultés; ne calcule pas H1 dans le script lu |
| [RATISS-ONE/Ratum](https://github.com/jonathansearch/RATISS-ONE) | associations non dirigées, succession dirigée, mémoire des liens | spécification du langage consultée; pas de test relancé ici |
| [RATISS-Bio](https://github.com/jonathansearch/ratiss-bio) | agrégat pondéré des persistances H1/H2, Xi_IDP, nuages biomoléculaires | README + `bio114/topology.py` consultés; entrée/agrégateur restent attachés à l’expérience |
| [RATISS-NEURO](https://github.com/jonathansearch/ratiss-neuro) | score de persistance H1 sur Takens, H2, graphe de plasticité | README + modules `topology.py` et `topo_plasticity.py` consultés; définitions séparées |
| [Crypto-net-veo-](https://github.com/jonathansearch/Crypto-net-veo-) | H1 max sur profils de corrélation; hystérésis, Kibble–Zurek, frustration | README + `ratiss_topo/topology.py` et `arsenal.py` consultés; canaux non homologiques typés séparément |
| [ratiss-Skynet](https://github.com/jonathansearch/ratiss-Skynet) | H1 max sur distance de corrélation d’activations | README + score et cœur scientifique consultés; mêmes unités/constructions à documenter par expérience |
| [RATISS Aeon Prime](https://github.com/jonathansearch/ratiss-aeon-agent) | Betti β0–β2 et score de risque annoncé sur surface d’attaque | README consulté; construction/fonction du score non exposées dans le passage lu |
| [synchrotron-24](https://github.com/jonathansearch/synchrotron-24) | H1 source = longueur max; conteneur H1+H2 total; winding/confinement | README, lois, protocoles, conteneur et scripts S03/S05 consultés; claims gardés comme résultats du modèle |
| [RATISS-QPU-AMBIENT](https://github.com/jonathansearch/RATISS-QPU-AMBIENT) | `P_sig` = rayon moyen de Bloch | README + `coherence.py` consultés; score géométrique, pas homologie |
| [QPU-Ratiss-COSMOS](https://github.com/jonathansearch/QPU-Ratiss-COSMOS) et [banc Grover](https://github.com/jonathansearch/Algorithmes-quantique-Ratiss-labs-) | association graphique, sidecar logique, flux de comptage et densité séparés | READMEs consultés; le réducteur précis du champ COSMOS reste à lier à sa version |
| [RATISS Quantum Topology Studio](https://github.com/jonathansearch/ratiss-topological-decoherence-engine) et [Studio Personal](https://github.com/jonathansearch/ratiss-decoherence-atlas) | graphe persistant, qubit logique, phase, twist, protection et route TSP séparés | README + guide algorithmique consultés; visualisation non prise pour preuve matérielle |
| [Ratiss-Fusion-stark-](https://github.com/jonathansearch/Ratiss-Fusion-stark-) | produit de confiance Needle × P_sig; solveur GUDHI/fallback | README + `topo_solver.py` consultés; branche GUDHI et fallback ne sont pas équivalents |
| [scientist-research-](https://github.com/jonathansearch/scientist-research-) et [portfolio](https://github.com/jonathansearch/Porte-folio-Jonathan-) | `Λ_LCT ∝ ∇P_sig`, noyau universel et équation de champ candidate | README consultés; unités, tenseur 4D et appui physique restent ouverts selon la source |
| [RATISS-PHOTON](https://github.com/jonathansearch/RATISS-PHOTON) | vortex de phase `±2π` avec gate d’amplitude; hypothèse de tension | spécification + campagne consultées; résultats explicitement bornés au simulateur |
| [RATISS-Jonathan-Labs](https://github.com/jonathansearch/Ratiss-Jonathan-Labs-) | P_sig d’un graphe d’affinité, Betti et route d’inspection distincts | README consulté; s’appuie sur le moteur topologique RATISS |
| [RATISS-NEURALINK-POC](https://github.com/jonathansearch/RATISS-Neuralink-POC) | classe `winding_class` de micro-cycles | README repéré; formule mathématique non extraite, laissée ouverte |
| RATISS-SIMULTANEITE, RATISS-GTT, RATISS-PLANCK | frontières entre synchronisation, invariants algébriques et formules physiques | README/fichiers ciblés; notés comme voisins, non assimilés à l’homologie |

## 6. Limite de cette édition

« Formulations existantes » signifie ici : formulations explicites retrouvées dans les sources indiquées. Le contrôle d’inventaire a porté sur les 97 dépôts publics recensés; 95 README ont été récupérés et les fichiers de code/documentation ont ensuite été consultés de façon ciblée pour les sources topologiques retenues. Il ne s’ensuit pas que chaque fichier ni chaque historique de chaque dépôt a été audité ligne par ligne. Une nouvelle occurrence pourra être ajoutée sans changer la règle centrale : **source exacte, structure construite, signature typée, statut et limite**.
