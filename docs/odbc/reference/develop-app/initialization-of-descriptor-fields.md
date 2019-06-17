---
title: Inizializzazione dei campi di descrizione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d988099cad357254f04a79a8a6cccbbe4eb2768c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446812"
---
# <a name="initialization-of-descriptor-fields"></a>Inizializzazione dei campi di descrizione
Quando si alloca un descrittore riga dell'applicazione, i relativi campi ricevano valori iniziali come indicato nella [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Il valore iniziale del campo SQL_DESC_TYPE è SQL_DEFAULT. Ciò consente un trattamento dei dati del database per la presentazione all'applicazione standard. L'applicazione può specificare diverse modalità di gestione dei dati impostando i campi del record del descrittore.  
  
 Il valore iniziale di SQL_DESC_ARRAY_SIZE nell'intestazione del descrittore è 1. L'applicazione può modificare questo campo per abilitare recupero di più righe.  
  
 Il concetto di un valore predefinito non è valido per i campi di un'implementazione. Un'applicazione può accedere ai campi di un'implementazione solo quando è presente un'istruzione preparata o eseguita associata.  
  
 Determinati campi di un IPD sono definiti solo dopo il IPD sono popolate automaticamente dal driver. In caso contrario, non sono definite. Questi campi sono SQL_DESC_CASE_SENSITIVE SQL_DESC_FIXED_PREC_SCALE, descrizione SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED e SQL_DESC_LOCAL_TYPE_NAME.
