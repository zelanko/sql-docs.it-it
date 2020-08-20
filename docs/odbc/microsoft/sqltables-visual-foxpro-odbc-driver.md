---
description: SQLTables (driver ODBC Visual FoxPro)
title: SQLTables (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 089208ab612984283e3f87c4ad03aca0ccfa2b38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471553"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 1  
  
 Restituisce l'elenco dei nomi di tabella specificati dal parametro nell'istruzione **SQLTables** . Se non viene specificato alcun parametro, restituisce i nomi di tabella archiviati nell'origine dati corrente. Il driver restituisce le informazioni come un set di risultati.  
  
 Le chiamate al tipo di enumerazione non riceveranno una voce del set di risultati per le visualizzazioni remote o le visualizzazioni con parametri locali. Tuttavia, una chiamata a **SQLTables** con un identificatore di nome di tabella univoco troverà una corrispondenza per tale vista se presente con lo stesso nome; Ciò consente di utilizzare l'API per verificare la presenza di conflitti di nome prima della creazione di una nuova tabella.  
  
> [!NOTE]  
>  Il driver ODBC Visual FoxPro distingue tra le [tabelle di database](../../odbc/microsoft/visual-foxpro-terminology.md) e le [tabelle gratuite](../../odbc/microsoft/visual-foxpro-terminology.md), anche quando entrambi i tipi di tabelle vengono archiviati nella stessa directory del sistema. Se l'origine dati è una directory di tabelle gratuite, il driver ODBC Visual FoxPro non cataloga né restituisce i nomi di tabelle associate a un database.  
  
 Per ulteriori informazioni, vedere [SQLTables](../../odbc/reference/syntax/sqltables-function.md) in *ODBC Programmer ' s Reference*.
