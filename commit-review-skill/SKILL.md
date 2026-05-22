---
name: commit-review-skill
description: >
  Performs a thorough code review of a Git commit and generates a structured Markdown report.
  Trigger this skill whenever the user uploads or pastes a commit file (.txt or raw diff),
  or mentions "review this commit", "review my diff", "analyse ce commit", "faire une review",
  "code review", or any variant. Also trigger when the user mentions having run `git show`,
  `git diff`, or `git log -p` and wants feedback. Works in French or English — always respond
  in the same language as the user. Output is always a downloadable `.md` file.
---

# Skill : Commit Review

## Objectif

Analyser un commit Git fourni sous forme de fichier texte (obtenu via `git show <hash> > commit.txt`)
et produire un rapport de code review complet au format Markdown, prêt à partager.

---

## Étapes à suivre

### 1. Détecter la langue

Répondre **dans la même langue que l'utilisateur** (français ou anglais).
Le rapport `.md` généré est également dans cette langue.

### 2. Lire le fichier commit

Le fichier peut être :
- Un fichier `.txt` uploadé (disponible sous `/mnt/user-data/uploads/`)
- Du texte collé directement dans le chat

Lire son contenu via `bash_tool` si c'est un fichier uploadé :
```bash
cat /mnt/user-data/uploads/<filename>.txt
```

### 3. Extraire les métadonnées

À partir de l'entête du commit, extraire :
- **Hash** du commit
- **Auteur** et **date**
- **Message de commit** (titre + description si présente)
- **Fichiers modifiés** (liste des `diff --git` détectés)
- **Taille du diff** : nombre approximatif de lignes ajoutées/supprimées

### 4. Analyser le diff

Parcourir chaque fichier modifié et évaluer :

#### ✅ Points forts (Strengths)
Identifier et expliquer les bonnes pratiques observées :
- Architecture propre, patterns bien utilisés
- Gestion des erreurs et de la résilience
- Bonne couverture de tests
- Lisibilité et clarté du code
- Respect des conventions du projet

#### 🔴 Bugs
Identifier les bugs réels ou potentiels :
- Race conditions, NPE, deadlocks
- Logique incorrecte, cas limites non gérés
- Problèmes de concurrence ou d'état partagé
Pour chaque bug : citer le code concerné, expliquer le problème, proposer une correction.

#### ⚠️ Points d'attention (Points of Attention)
Signaler les problèmes non bloquants mais importants :
- Incohérences de configuration
- Nommage trompeur ou ambigu
- Comportements subtils inattendus
- Overhead inutile (ex: annotations lourdes sur tests unitaires)
- Dette technique introduite
Pour chaque point : citer le code, expliquer l'impact, recommander une action.

#### ℹ️ Suggestions mineures (optional)
Améliorations stylistiques ou de lisibilité sans impact fonctionnel.

### 5. Générer le fichier Markdown

Créer le fichier de review avec le nom : `review-<commit-short-hash>.md`
Sauvegarder dans `/mnt/user-data/outputs/`.

---

## Structure du fichier Markdown généré

```markdown
# Code Review — <TICKET-ID>: <Feature Title>

**Commit:** `<full hash>`
**Author:** <author>
**Date:** <date>
**Feature:** <brief description inferred from commit message and diff>

---

## Summary

<2-4 sentences describing what this commit does overall.>

---

## ✅ Strengths

### 1. <Title>
```<language>
<relevant code snippet>
```
<Explanation of why this is a good pattern.>

[repeat for each strength]

---

## 🔴 Bugs

### Bug 1: <Title>
```<language>
<relevant code snippet showing the problem>
```
<Explanation of the bug and its impact.>

> **Recommendation:** <concrete fix with code example if possible>

[repeat for each bug]

---

## ⚠️ Points of Attention

### 1. <Title>
```<language>
<relevant code snippet>
```
<Explanation.>

> **Recommendation:** <action to take>

[repeat for each point]

---

## 📋 Summary Table

| Area | Status | Comment |
|------|--------|---------|
| <aspect> | ✅ / 🔴 / ⚠️ / ℹ️ | <brief comment> |
...

---

## Overall Assessment

**Score: X / 10**

<2-4 sentence overall assessment: quality, risks, what to fix before merge.>
```

---

## Règles importantes

- **Toujours citer le code** concerné avant d'expliquer un problème.
- **Toujours proposer une correction** pour les bugs et points d'attention.
- **Ne pas inventer** de bugs qui ne sont pas visibles dans le diff.
- Si le diff est anonymisé (noms de classes remplacés), analyser la **structure et les patterns** plutôt que les noms.
- Si le diff est **incomplet ou tronqué**, le mentionner dans le Summary.
- Le score `/10` doit être justifié dans l'évaluation globale.
- **Ne jamais afficher le rapport dans le chat** — toujours générer le fichier `.md` et le présenter via `present_files`.

---

## Inférence du ticket / feature name

Le message de commit suit souvent le format : `feat(scope): TICKET-1234 description`
- Extraire l'ID de ticket (ex: `FEATURE-2786`, `PROJ-123`)
- Utiliser `FEATURE-XXXX` si non trouvé
- Inférer le nom de la feature depuis le message + les noms de fichiers modifiés

---

## Langues

| Langue détectée | Langue du rapport |
|-----------------|-------------------|
| Français        | Français          |
| Anglais         | Anglais           |
| Autre           | Anglais (défaut)  |

Les titres de sections (`✅ Strengths`, `🔴 Bugs`, etc.) sont traduits selon la langue :

| EN | FR |
|----|----|
| Strengths | Points forts |
| Bugs | Bugs |
| Points of Attention | Points d'attention |
| Summary Table | Tableau récapitulatif |
| Overall Assessment | Évaluation globale |
