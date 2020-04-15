---
title: Limitazioni dell'istruzione CREATE INDEX Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280882"
---
# <a name="create-index-statement-limitations"></a>Limitazioni dell'istruzione CREATE INDEX
L'istruzione CREATE INDEX non è supportata per i driver di Microsoft Excel o di testo.  
  
 Un indice può essere definito su un massimo di 10 colonne. Se in un'istruzione CREATE INDEX sono incluse più di 10 colonne, l'indice non verrà riconosciuto e la tabella verrà considerata come se non fosse stato creato alcun indice.  
  
 Il driver dBASE non è in grado di creare un indice in una colonna LOGICAL.  
  
 Quando viene utilizzato il driver dBASE, è possibile migliorare il tempo di risposta su file di grandi dimensioni creando un indice con estensione mdx (o ndx) nella colonna (campo) specificata nelle clausole WHERE di un'istruzione SELECT. Gli indici .mdx esistenti verranno applicati automaticamente \<per gli operatori , > , , >,< e BETWEEN in una clausola WHERE e nei predicati LIKE, nonché nei predicati join.  
  
 Quando viene utilizzato il driver dBASE, l'indice creato da un'istruzione CREATE UNIQUE INDEX è in realtà non univoco e i valori duplicati possono essere inseriti nella colonna indicizzata. È possibile aggiungere all'indice un solo record di un set con valori di chiave identici.  
  
 Quando viene utilizzato il driver Paradox, è necessario definire un indice univoco su un subset contiguo delle colonne di una tabella, inclusa la prima colonna. Una tabella non può essere aggiornata dal driver Paradox se non è definito un indice univoco nella tabella o quando il driver Paradox viene utilizzato senza l'implementazione del motore di database Borland.
