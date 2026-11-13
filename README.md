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
| `meteo` | weather-forecast | animation selon la météo |
| `aspirateur` | tile (vacuum) | couleur + animation selon l'état |
| `aspirateur-carte` | picture-entity (plan) | intégration du plan dans le thème |

Des exemples complets sont dans le dossier [`exemples/`](exemples/).
