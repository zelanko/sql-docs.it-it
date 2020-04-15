---
title: Associazione di colonne per l'utilizzo con i cursori di blocco . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e527658a7d6945921510de898c648075c41fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284901"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Associazione di colonne per l'uso con cursori rettangolari
Poiché i cursori a blocchi restituiscono più righe, le applicazioni che li utilizzano devono associare una matrice di variabili a ogni colonna anziché a una singola variabile. Queste matrici sono note collettivamente come *buffer di set di righe*. Di seguito sono riportati i due stili di associazione:  
  
-   Associare una matrice a ogni colonna. Questa operazione è denominata *associazione per colonna* perché ogni struttura di dati (matrice) contiene dati per una singola colonna.  
  
-   Definire una struttura per contenere i dati per un'intera riga e associare una matrice di queste strutture. Questa operazione viene definita *associazione per riga* perché ogni struttura di dati contiene i dati per una singola riga.  
  
 Come quando l'applicazione associa singole variabili alle colonne, chiama **SQLBindCol** per associare le matrici alle colonne. L'unica differenza è che gli indirizzi passati sono indirizzi di matrice, non indirizzi di singole variabili. L'applicazione imposta l'attributo di istruzione SQL_BIND_BY_COLUMN per specificare se utilizza l'associazione per colonna o per riga. Se utilizzare l'associazione per colonna o per riga è in gran parte una questione di preferenza dell'applicazione. L'associazione per riga potrebbe corrispondere più strettamente al layout dei dati dell'applicazione, nel qual caso fornirebbe prestazioni migliori.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione basata su colonneColumn-Wise Binding](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associazione basata su righe](../../../odbc/reference/develop-app/row-wise-binding.md)
