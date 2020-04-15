---
title: 'Conteggio dei record : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281817"
---
# <a name="record-count"></a>Conteggio record
Il campo di intestazione SQL_DESC_COUNT di un descrittore è l'indice in base uno del record con il numero più alto che contiene dati. Questo campo non è un conteggio di tutte le colonne o i parametri associati. Quando viene allocato un descrittore, il valore iniziale di SQL_DESC_COUNT è 0.  
  
 Il driver esegue tutte le azioni necessarie per allocare e gestire lo spazio di archiviazione necessario per contenere le informazioni sul descrittore. L'applicazione non specifica in modo esplicito le dimensioni di un descrittore né alloca nuovi record. Quando l'applicazione fornisce informazioni per un record descrittore il cui numero è superiore al valore di SQL_DESC_COUNT, il driver aumenta automaticamente SQL_DESC_COUNT. Quando l'applicazione annulla l'associazione del record descrittore con il numero più alto, il driver riduce automaticamente SQL_DESC_COUNT contenere il numero del record associato più alto rimanente.
