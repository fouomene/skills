---
name: rephrasing-skill
description: >
  Reformule et améliore un texte en français ou en anglais pour le rendre naturel et fluide.
  Utiliser ce skill dès que l'utilisateur demande de "reformuler", "réécrire", "améliorer",
  "corriger le style" ou "nettoyer" un texte — en particulier les textes traduits via Google
  Translate ou un autre outil automatique. Fonctionne sur tous types de contenus : emails,
  courriers, documents techniques, phrases isolées. Déclencher aussi si l'utilisateur colle
  un texte qui semble maladroit, peu naturel, ou traduit mot à mot, même sans demande explicite
  de reformulation. Ne pas hésiter à utiliser ce skill dès qu'un texte gagnerait à être fluidifié.
---

# Skill : Reformulation de texte (Rephrasing)

## Objectif

Reformuler un texte en anglais ou en français pour le rendre **naturel, fluide et idiomatique**,
tout en préservant fidèlement le sens original. Ce skill est particulièrement utile pour les
textes issus de traductions automatiques (Google Translate, DeepL, etc.) qui sonnent mécaniques
ou peu naturels.

---

## Étapes à suivre

### 1. Détecter la langue

Identifier automatiquement si le texte est en **français** ou en **anglais**.
Si la langue est ambiguë ou mixte, reformuler dans la langue dominante et le mentionner.

### 2. Analyser les problèmes du texte

Avant de reformuler, repérer mentalement :
- Tournures calquées mot à mot sur une autre langue
- Répétitions inutiles ou maladresses stylistiques
- Ponctuation ou structure de phrases non naturelles
- Registre incohérent (mélange formel/familier)
- Vocabulaire trop littéral ou peu idiomatique

### 3. Reformuler

Appliquer les règles suivantes selon la langue :

**En français :**
- Privilégier les constructions naturelles du français (pas de calques de l'anglais)
- Respecter les règles typographiques françaises (espaces avant `?`, `!`, `:`, `«»`, etc.)
- Adapter les expressions idiomatiques (ne pas traduire "make sense" par "faire du sens")
- Conserver le registre d'origine (formel, professionnel, neutre)

**En anglais :**
- Utiliser des tournures idiomatiques naturelles
- Éviter les constructions rigides calquées sur le français
- Adapter le registre (formal/informal) selon le contexte
- Préférer des phrases actives et directes quand c'est possible

### 4. Présenter le résultat

Présenter la version reformulée **clairement**, dans un bloc distinct.

- Pour les textes courts (< 5 phrases) : reformuler directement, sans commentaire superflu.
- Pour les textes plus longs ou techniques : reformuler puis **brièvement signaler** (en 1-2 lignes)
  les principaux types de corrections apportées (ex: "Suppression des calques anglais, fluidification
  des transitions, harmonisation du registre formel.").
- Ne pas proposer de variantes sauf si l'utilisateur le demande explicitement.
- Ne pas expliquer chaque modification phrase par phrase sauf demande explicite.

---

## Exemples de corrections typiques (textes traduits)

| Texte brut (Google Translate)            | Reformulé naturellement                    |
|------------------------------------------|--------------------------------------------|
| "Ça ne fait pas de sens."                | "Ça n'a pas de sens."                      |
| "Je suis disponible pour une réunion."   | "Je suis disponible pour une réunion." ✓   |
| "Suite à votre email ci-dessous..."      | "Faisant suite à votre message..."         |
| "Please find attached the document."    | "Please find the document attached."  ✓    |
| "We are in receipt of your request."    | "We have received your request."           |
| "Il a mentionné que le projet est bon." | "Il a indiqué que le projet était satisfaisant." |

---

## Comportement selon le type de contenu

| Type de texte        | Comportement attendu                                                   |
|----------------------|------------------------------------------------------------------------|
| Email / courrier     | Respecter la structure (objet, formule d'appel, corps, formule de politesse) |
| Document technique   | Priorité à la clarté et à la précision ; éviter le jargon inutile     |
| Phrase isolée        | Reformulation directe, concise, sans commentaire                       |

---

## Ce que ce skill ne fait PAS

- Il ne traduit pas (il reformule dans la langue d'origine du texte)
- Il ne résume pas le texte
- Il ne change pas le sens ou les informations factuelles
- Il ne corrige pas les erreurs factuelles (dates, noms, chiffres)
