---
date: 2007-05-30 21:04:00
layout: post
redirect_from: "post/2007/05/30/Mise-a-jour-dune-table-a-partir-dune-autre"
tags: code-snippets, sql
title: "Mise à jour d'une table à partir d'une autre"
---

Pour mettre à jour un champ d'une table à partir du champ équivalent d'une
autre table, Access accepte deux noms de tables pour la commande UPDATE, mais
pas Sql Server.

Exemple : les taux de TVA ayant été corrigés dans la table des
articles, il faut répercuter ces modifications dans la table des lignes de
factures

Sous Access

```
UPDATE LignesFactures, Articles
SET    LignesFactures.TauxTva = Articles.TauxTva
WHERE  LignesFactures.ArticleID = Articles.ArticleID
```

Sous Sql Server

```
UPDATE LignesFactures
SET    LignesFactures.TauxTva = Articles.TauxTva
FROM   LignesFactures
INNER JOIN Articles ON Articles.ArticleID = LignesFactures.ArticleID
```

Mise à jour : Sous Oracle

```
UPDATE LignesFactures
SET    LignesFactures.TauxTva = (SELECT Articles.TauxTva
                                 FROM   Articles
                                 WHERE  Articles.ArticleID = LignesFactures.ArticleID)
```
