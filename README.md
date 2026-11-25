# S_theme

Thème sombre et épuré pour Home Assistant : cards en dégradé, couleurs qui
changent selon l'état des entités, animations douces.

## Prérequis

- [card-mod](https://github.com/thomasloven/lovelace-card-mod) (HACS), chargé
  via `extra_module_url` dans `configuration.yaml`
- Pour certaines cards : `mini-graph-card`, `bar-card` (HACS)

```yaml
frontend:
  themes: !include_dir_merge_named themes
  extra_module_url:
    - /local/community/lovelace-card-mod/card-mod.js
```

## Installation (HACS)

1. HACS → menu ⋮ → **Dépôts personnalisés**
2. URL : `https://github.com/Sown21/HA_Theme`, type : **Thème**
3. Télécharger **S_theme**, puis lancer l'action `frontend.reload_themes`
4. Profil → Thème → **S_theme**

## Classes disponibles

À ajouter dans une card avec :

```yaml
card_mod:
  class: <classe>
```

| Classe | Card | Effet |
|---|---|---|
| `prise` | tile (switch) | lueur jaune quand allumé |
| `tempo` | tile (couleur Tempo) | teinte Bleu / Blanc / Rouge |
| `tempo-jours` | bar-card | barres arrondies animées |
| `climat` | mini-graph-card | teinte selon la température |
| `solaire` | mini-graph-card | intensité selon la production |
| `meteo` | weather-forecast | animation réaliste selon la météo (voir [détail](#animations-météo)) |
| `aspirateur` | tile (vacuum) | couleur + animation selon l'état |
| `aspirateur-carte` | picture-entity (plan) | intégration du plan dans le thème |
| `volet` | tile (cover) | lames selon la position, défilement en mouvement |
| `chauffage` | tile (climate) | air chaud qui monte quand ça chauffe, éco vert, clim givrée |

Des exemples complets sont dans le dossier [`exemples/`](exemples/).

## Animations météo

La classe `meteo` choisit l'animation selon l'état de l'entité `weather` :

| État | Animation |
|---|---|
| `sunny` | soleil dans le coin, rayons qui tournent lentement, halo qui respire |
| `clear-night` | ciel étoilé qui scintille, étoile filante, clair de lune derrière l'icône |
| `partlycloudy` | soleil + nuages qui passent devant |
| `cloudy` | nuages en relief sur 2 plans (parallaxe) |
| `fog` | voile laiteux + filaments de brume qui dérivent, plus denses au sol |
| `windy` | filets d'air par rafales + feuilles qui tournoient |
| `windy-variant` | vent + nuages poussés en arrière-plan |
| `rainy` / `pouring` | gouttes effilées sur 2 plans + éclaboussures (averse plus dense et rapide) |
| `hail` | pluie + grêlons qui tombent vite et rebondissent |
| `lightning` / `lightning-rainy` | éclairs ramifiés à rythme irrégulier, flash bleuté (+ pluie) |
| `snowy` / `snowy-rainy` | flocons ❄ qui tombent en se balançant |

**Gel** : Home Assistant n'a pas d'état « gel ». Il est déduit de l'attribut
`temperature` de l'entité (≤ 0 °C, ou ≤ 32 °F). Par temps sec, le givre
remplace l'animation : teinte cyan, givre dans les coins et cristaux ❄ figés
qui scintillent. Sous la pluie ou la neige, seul un bord givré s'ajoute.

Les animations respectent le réglage système « réduire les animations ».

Pour tester un état sans attendre la bonne météo : *Outils de développement →
États*, choisir l'entité `weather`, modifier l'état (et l'attribut
`temperature` pour le gel), puis « Définir l'état ».
