# Skills de Hamza

Collection de mes skills personnels pour [Claude Code](https://claude.com/claude-code), distribuée sous forme de plugin.

## Installation

Dans Claude Code :

```text
/plugin marketplace add hamzaiqbal/skills
/plugin install hamza-iqbal-skills@hamza-iqbal-skills
```

## Structure du dépôt

```text
.
├── .claude-plugin/
│   ├── plugin.json         # Manifeste du plugin
│   └── marketplace.json    # Catalogue permettant l'installation via /plugin
├── skills/
│   └── <nom-du-skill>/
│       └── SKILL.md        # Un dossier par skill
├── LICENSE
└── README.md
```

## Ajouter un skill

1. Créer un dossier `skills/<nom-du-skill>/` (nom en minuscules, avec des tirets).
2. Y ajouter un fichier `SKILL.md` avec un en-tête YAML :

   ```markdown
   ---
   name: nom-du-skill
   description: Quand et pourquoi utiliser ce skill. Soit précis sur les déclencheurs.
   ---

   # Nom du skill

   Instructions détaillées pour Claude.
   ```

3. Si besoin, ajouter à côté de `SKILL.md` des fichiers de référence, scripts ou modèles.
4. Incrémenter la `version` dans `.claude-plugin/plugin.json`.

## Bonnes pratiques

- **Une description claire** : c'est elle qui permet à Claude de décider quand activer le skill.
- **Un skill, une responsabilité** : mieux vaut plusieurs skills ciblés qu'un seul fourre-tout.
- **Détails à la demande** : garder `SKILL.md` concis et déporter le reste dans des fichiers annexes.
- **Pas de secrets** dans le dépôt.

## Skills disponibles

| Skill | Rôle |
| --- | --- |
| `humanizer` | Retire les marqueurs de texte généré par IA pour un rendu plus naturel. |
| `langage-clair` | Réécrit ou évalue un texte en langage clair. |
| `redaction-style` | Rédige des posts LinkedIn dans le style de Hamza Iqbal. |
| `structure-transcript` | Nettoie et structure une transcription vocale ou une dictée. |
| `tldr` | Résume un document, un texte ou une page web en français. |

## Licence

[MIT](LICENSE)
