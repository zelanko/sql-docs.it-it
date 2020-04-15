---
title: SQLExecDirect (Driver ODBC di Visual FoxPro) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298671"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello di baseODBC API Conformance: Core Level  
  
 Esegue una nuova [istruzione SQL preparabile](../../odbc/microsoft/visual-foxpro-terminology.md). Il driver ODBC di Visual FoxPro utilizza i valori correnti delle variabili del marcatore di parametro se esistono parametri nell'istruzione.  
  
 Per creare un comando batch per inviare più di un'istruzione SQL alla volta, utilizzare un punto e virgola (;) per separare ogni istruzione SQL nel batch.  
  
 Se i nomi di tabella, vista o campo contengono spazi, racchiudere i nomi tra virgolette rovesciate. Ad esempio, se il database contiene una tabella denominata Tabella personale e il campo Campo personale, racchiudere ogni elemento dell'identificatore come segue:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Per ulteriori informazioni, vedere [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) in *ODBC Programmer's Reference*.
