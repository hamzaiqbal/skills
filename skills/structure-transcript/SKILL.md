---
name: "structure-transcript"
description: "Nettoie et structure une transcription vocale ou une dictée, sans rien inventer. Si une image est jointe, elle sert à vérifier la cohérence. Corrige les erreurs de reconnaissance évidentes, signale les passages douteux, pose des questions si contradiction. Format de sortie donné dans la conversation."
---

# Structure transcript

Tu reçois la transcription brute d'un propos oral. Tu la reformules sans changer le sens.

**Principe.** Fidélité d'abord. Tu retires le bruit et tu gardes ce qui porte du sens. Tu n'ajoutes ni information, ni remarque d'expert, ni recommandation non demandée.

## Image jointe (si présente)

Si une image (capture d'écran, maquette, schéma) accompagne la transcription, regarde-la avant l'étape 1. Elle sert à vérifier la cohérence, pas à compléter le texte.

- Compare chaque affirmation de l'orateur avec ce que l'image montre : éléments, nombre, ordre, libellés, états.
- Utilise les textes visibles dans l'image pour lever un doute de reconnaissance vocale (nom propre, libellé, sigle).
- Ne reprends jamais dans le texte final une information qui est seulement dans l'image. L'orateur reste la seule source des règles.
- Un écart entre la transcription et l'image est une contradiction : traite-le à l'étape 1 s'il change le résultat.

## Étape 1 : chercher les contradictions (avant tout)

Lis toute la transcription. Repère :

- les contradictions entre deux passages (ex. deux conteneurs différents pour le même élément) ;
- les ambiguïtés qui changent le résultat (deux lectures possibles, donnée indispensable manquante) ;
- les passages inaudibles ou incohérents dont dépend la sortie ;
- les écarts entre la transcription et l'image jointe (nombre d'éléments, ordre, libellé, élément décrit mais absent de l'image) qui changent le résultat.

Si tu en trouves :

1. **Ne génère rien**, pas même un brouillon.
2. Pose une question courte par point bloquant, avec les lectures possibles en choix fermés. Utilise l'outil de questions (AskUserQuestion) s'il est disponible, sinon pose-les en texte.
3. Attends les réponses, puis génère.

Ne sont pas des contradictions :

- une auto-correction claire (« non, plutôt X ») : la dernière version prime ;
- un doute mineur qui ne change pas le sens : choisis la lecture la plus probable et note-la dans la ligne « Hypothèse retenue ».

## Étape 2 : nettoyer

Retire :

- les hésitations (« euh », « ben », « du coup », « en fait » vides de sens) et les tics d'oral (« tu vois », « voilà », « quoi ») ;
- les répétitions, faux départs et phrases abandonnées (garde la version finale) ;
- les digressions sans lien avec l'objectif.

Ne retire pas un mot oral qui porte du sens (une nuance, une restriction, une condition).

Corrige la ponctuation et les phrases mal découpées.

## Étape 3 : corriger les erreurs de reconnaissance vocale

Corrige un terme (homophone, nom propre ou terme technique déformé, sigle épelé lettre par lettre) seulement si le contexte lève le doute. Un texte visible dans l'image jointe compte comme contexte. Note chaque correction non triviale dans « Hypothèse retenue ».

Si un terme reste douteux et ne bloque pas la sortie :

- garde-le tel quel et marque-le `[? terme à vérifier]` ;
- ne le supprime jamais : l'utilisateur doit voir où est le trou ;
- ne le devine pas.

Si le terme douteux bloque la sortie, reviens à l'étape 1 et pose la question.

## Étape 4 : structurer

- Regroupe par sens. Si l'orateur annonce un ordre (« dans l'ordre »), respecte-le.
- Une idée par phrase, voix active, verbes plutôt que noms.
- Un même objet garde le même nom. Garde le vocabulaire de l'orateur.
- Garde la raison d'une règle quand l'orateur la donne (« car si… »), en une courte proposition.
- Fournis l'exemple demandé (code, texte, tableau), fidèle à la description et commenté si c'est du code.

## Format de sortie

L'utilisateur donne le format dans la conversation (prompt, mail, note, spécifications, compte rendu, etc.). Applique les étapes 1 à 4, puis adapte la forme.

Sans indication, utilise cette structure :

1. `# Contexte / Zone` : périmètre du propos, sous la forme « Contexte / Zone » ou « Transverse / Sujet ».
2. `## Sujet` : un titre par sujet traité.
3. Une phrase d'intro sous chaque `##` : l'enjeu en une ligne.
4. Les règles ou points clés en puces, une par puce, dans l'ordre dicté.
5. Les détails et sous-conditions en sous-puces.
6. Les termes techniques (balises, attributs, commandes, noms de fichiers, etc.) en `code`, avec la casse exacte.
7. L'exemple demandé : bloc sous la liste.
8. « Écarts avec l'image » : seulement si une image est jointe et qu'un écart non bloquant existe. Liste factuelle : ce que l'orateur dit et que l'image ne montre pas, ou l'inverse. N'en fais ni une critique ni une règle.
9. « Hypothèse retenue » : dernière ligne, seulement s'il y en a une.

```
# Contexte / Zone
## Sujet
Phrase d'intro : l'enjeu en une ligne.

* Point 1
* Point 2
   * Détail ou sous-condition
```

## Contrôle final (avant d'envoyer)

Vérifie en une passe :

- aucune information, décision, chiffre, nom ou date n'a été ajouté ni modifié ;
- rien d'important de la transcription n'a disparu ;
- chaque terme douteux est corrigé (avec note) ou marqué `[? …]` ;
- chaque écart avec l'image jointe est traité (question, hypothèse ou liste « Écarts avec l'image ») ;
- le format correspond à la demande.

## Journal des modifications (sur demande)

Si l'utilisateur le demande, ajoute sous le texte un journal court : ce qui a été retiré (catégories et nombre), les corrections vocales faites, les passages marqués `[? …]`.

## Règles

- Ne renvoie ni la transcription d'origine ni le détail de ton travail, sauf demande.
- Ne change jamais une décision, un chiffre, un nom ou une date.
- Garde la langue, le ton et la personne grammaticale de l'orateur (« je », « on »), sauf demande contraire.
- N'ajoute aucune critique ni amélioration. Si l'utilisateur veut un avis d'expert, il le demandera.