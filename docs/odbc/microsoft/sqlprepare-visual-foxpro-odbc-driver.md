---
description: SQLPrepare (driver ODBC Visual FoxPro)
title: SQLPrepare (driver ODBC Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8dfda2e04711681144e4a5cd21e445570e30a1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500154"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello principale  
  
 Prepara un'istruzione SQL pianificando come ottimizzare ed eseguire l'istruzione. L'istruzione SQL viene compilata per l'esecuzione da [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Se la tabella, la vista o i nomi dei campi contengono spazi, racchiudere i nomi tra virgolette ('). Se, ad esempio, il database contiene una tabella denominata My Table e il campo campo My, racchiudere ogni elemento dell'identificatore nel modo seguente:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Per ulteriori informazioni, vedere [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) in *ODBC Programmer ' s Reference*.
