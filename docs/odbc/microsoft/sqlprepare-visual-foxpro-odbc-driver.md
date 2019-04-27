---
title: SQLPrepare (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3ef083829b1ce322f2cede53f853c80683f01cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636670"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: A livello centrale  
  
 Prepara un'istruzione SQL, pianificare come ottimizzare ed eseguire l'istruzione. L'istruzione SQL viene compilata per l'esecuzione dal [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Se la tabella, vista o i nomi dei campi contengono spazi, racchiudere i nomi tra backup racchiudere tra virgolette singole ('). Ad esempio, se il database contiene una tabella denominata tabella personale e il campo My Field, racchiudere tra ogni elemento dell'identificatore come indicato di seguito:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Per altre informazioni, vedere [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) nel *riferimento per programmatori ODBC*.
