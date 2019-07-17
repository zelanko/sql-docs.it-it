---
title: SQLExecDirect (Driver ODBC Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e701340217a885fbf1e3372c33ed1a8cfdb21457
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053854"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: A livello centrale  
  
 Esegue un nuovo [istruzione SQL preparabile](../../odbc/microsoft/visual-foxpro-terminology.md). Il Driver ODBC Visual FoxPro Usa i valori correnti delle variabili di marcatore di parametro, se sono presenti parametri nell'istruzione.  
  
 Per creare un comando di batch per inviare più di un'istruzione SQL in un momento, usare un punto e virgola (;) per separare ogni istruzione SQL del batch.  
  
 Se la tabella, vista o i nomi dei campi contengono spazi, racchiudere i nomi tra backup preventivo contrassegni. Ad esempio, se il database contiene una tabella denominata tabella personale e il campo My Field, racchiudere tra ogni elemento dell'identificatore come indicato di seguito:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Per altre informazioni, vedere [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) nel *riferimento per programmatori ODBC*.
