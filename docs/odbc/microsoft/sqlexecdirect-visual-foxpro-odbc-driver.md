---
title: SQLExecDirect (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298671"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello principale  
  
 Esegue una nuova [istruzione SQL preparabile](../../odbc/microsoft/visual-foxpro-terminology.md). Il driver ODBC Visual FoxPro usa i valori correnti delle variabili del marcatore di parametro se nell'istruzione sono presenti parametri.  
  
 Per creare un comando batch per inviare più istruzioni SQL alla volta, usare un punto e virgola (;) per separare ogni istruzione SQL nel batch.  
  
 Se i nomi di tabella, vista o campo contengono spazi, racchiudere i nomi tra virgolette. Se, ad esempio, il database contiene una tabella denominata My Table e il campo campo My, racchiudere ogni elemento dell'identificatore nel modo seguente:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Per ulteriori informazioni, vedere [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) in *ODBC Programmer ' s Reference*.
