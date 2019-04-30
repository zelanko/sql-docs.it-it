---
title: Limitazioni dell'istruzione dell'indice CREATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec6ba27197f7a6021aff90d30884129128cb3614
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232280"
---
# <a name="create-index-statement-limitations"></a>Limitazioni dell'istruzione CREATE INDEX
L'istruzione CREATE INDEX non è supportata per i driver di Microsoft Excel o di testo.  
  
 È possibile definire un indice su un massimo di 10 colonne. Se più di 10 colonne sono incluse in un'istruzione CREATE INDEX, l'indice non verrà riconosciuta e la tabella verrà considerata come se non include un indice sono stati creati.  
  
 Il driver dBASE non è possibile creare un indice su una colonna LOGICA.  
  
 Quando viene usato il driver dBASE, tempo di risposta nel file di grandi dimensioni può essere migliorata creando un indice (con estensione MDX o ndx) nella colonna (campo) specificato nelle clausole WHERE di un'istruzione SELECT. Gli indici con estensione MDX esistenti verranno applicati automaticamente per =, >, \<, > =, = < e tra gli operatori in una clausola WHERE e predicati LIKE, nonché nei predicati di join.  
  
 Quando viene usato il driver dBASE, l'indice creato da un'istruzione CREATE UNIQUE INDEX è effettivamente non univoci e possono essere inseriti valori duplicati nella colonna indicizzata. Un solo record da un set con gli stessi valori di chiave può essere aggiunto all'indice.  
  
 Quando viene usato il driver Paradox, è necessario definire un indice univoco su un subset delle colonne in una tabella, incluse la prima colonna contiguo. Impossibile aggiornare una tabella dal driver Paradox se un indice univoco non è definito nella tabella o quando il driver Paradox viene usato senza l'implementazione del motore di Database Borland.
