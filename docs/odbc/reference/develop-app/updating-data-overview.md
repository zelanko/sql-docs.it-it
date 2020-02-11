---
title: Panoramica sull'aggiornamento dei dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0701218b5ef489d1f8962ffadc9409986a0c36c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942818"
---
# <a name="updating-data-overview"></a>Panoramica sull'aggiornamento dei dati
Le applicazioni possono aggiornare i dati tramite l'esecuzione di istruzioni SQL o la chiamata a **SQLSetPos** o **SQLBulkOperations**. Le istruzioni **Update**, **Delete**e **Insert** agiscono direttamente sull'origine dati e sono in genere supportate dai driver. Le istruzioni Update e Delete ricercate contengono una specifica delle righe da modificare. Le istruzioni Update e Delete posizionate e **SQLSetPos** agiscono sull'origine dati attraverso un cursore e sono meno ampiamente supportate.  
  
 Indica se i cursori possono rilevare le modifiche apportate al set di risultati con i metodi descritti in questa sezione dipendono dal tipo di cursore e dalla relativa modalità di implementazione. I cursori di sola trasmissione non rivisitano le righe e pertanto non rileveranno alcuna modifica. Per informazioni sul fatto che i cursori scorrevoli possano rilevare le modifiche, vedere [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Istruzioni UPDATE, DELETE e INSERT](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulazione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinazione del numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Aggiornamento dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Dati di tipo Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
