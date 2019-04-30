---
title: Tipi di dati C predefiniti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c4147b1bfa5ffb1e379c3aa8be2c9ea2a9d2775
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240965"
---
# <a name="default-c-data-types"></a>Tipi di dati C predefiniti
Se un'applicazione specifica SQL_C_DEFAULT nelle **SQLBindCol**, **SQLGetData**, o **SQLBindParameter**, il driver presuppone che tipo di dati C del buffer di input o output corrisponde al tipo di dati SQL della colonna o del parametro a cui è associato il buffer.  
  
> [!IMPORTANT]  
>  Applicazioni interoperative non devono utilizzare SQL_C_DEFAULT. Al contrario, questi devono sempre specificare il tipo di C del buffer in uso. Infatti, i driver non possono determinare sempre correttamente il tipo C predefinito, per i motivi seguenti:  
  
-   Se il sistema DBMS Alza di livello un tipo di dati SQL di una colonna o parametro, il driver non è possibile determinare il tipo di dati SQL originale di una colonna o parametro. Pertanto, non può determinare il tipo di dati C predefinito corrispondente.  
  
-   Se il driver non è possibile determinare se è firmato una determinata colonna o un parametro, come accade spesso quando si tratta di gestito dal sistema DBMS, il driver non è possibile determinare se il tipo di dati C predefiniti corrispondenti deve essere firmato o senza segno.  
  
     Poiché SQL_C_DEFAULT viene fornito solo per motivi di praticità programmazione, l'applicazione non vengono perse tutte le funzionalità quando si specifica il tipo di dati C effettivo.  
  
 Una tabella che mostra il tipo di dati C predefiniti per ogni tipo di dati SQL è inclusa nella [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md), più avanti in questa appendice.
