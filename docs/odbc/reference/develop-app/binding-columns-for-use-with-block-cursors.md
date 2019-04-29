---
title: Associazione di colonne per l'utilizzo con cursori a blocchi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0ed819643e7ea818fc17c0fa317473afc8f5ca3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007866"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Associazione di colonne per l'uso con cursori rettangolari
Poiché i cursori a blocchi di restituire più righe, le applicazioni che li utilizzano necessario associare una matrice di variabili a ogni colonna anziché una singola variabile. Questi array sono noti collettivamente come le *set di righe buffer*. Di seguito sono i due stili di binding:  
  
-   Associare una matrice per ogni colonna. Questa operazione viene definita *associazione per colonna* perché ogni struttura di data (array) contiene i dati per una singola colonna.  
  
-   Definire una struttura per contenere i dati per un'intera riga e associare una matrice di queste strutture. Questa operazione viene definita *l'associazione per riga* perché ogni struttura di dati contiene i dati per una singola riga.  
  
 Quando l'applicazione associa le variabili sola alle colonne, che chiama **SQLBindCol** per associare le matrici di colonne. L'unica differenza è che gli indirizzi inoltrati sono matrice indirizzi, non singola variabile. L'applicazione imposta l'attributo di istruzione SQL_BIND_BY_COLUMN per specificare se utilizza l'associazione per colonna o per riga. Se si desidera utilizzare l'associazione per colonna o per riga è in gran parte di una questione di preferenza dell'applicazione. L'associazione per riga potrebbero corrispondere più da vicino al layout dell'applicazione dei dati, nel qual caso offrirà prestazioni migliori.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione per colonna](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associazione per riga](../../../odbc/reference/develop-app/row-wise-binding.md)
