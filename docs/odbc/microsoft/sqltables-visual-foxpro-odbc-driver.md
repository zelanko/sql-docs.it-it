---
title: SQLTables (Driver ODBC Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e134b2870c4506e725f2900b83d1118e42b55d15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63219116"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 1  
  
 Restituisce l'elenco di nomi di tabella specificato dal parametro di **SQLTables** istruzione. Se si specifica alcun parametro, restituisce i nomi di tabella archiviati nell'origine dati corrente. Il driver restituisce le informazioni come set di risultati.  
  
 Le chiamate di tipo di enumerazione non riceveranno una voce del set di risultati per visualizzazioni remote o locale con parametri. Tuttavia, una chiamata a **SQLTables** con una tabella univoca identificatore di nome verrà trovata una corrispondenza per una visualizzazione di questo tipo se è presente con lo stesso nome; in questo modo l'API da usare per verificare la presenza di conflitti di nome prima della creazione di una nuova tabella.  
  
> [!NOTE]  
>  Il driver ODBC Visual FoxPro distingue [tabelle di database](../../odbc/microsoft/visual-foxpro-terminology.md) e [libero tabelle](../../odbc/microsoft/visual-foxpro-terminology.md), anche quando entrambi i tipi di tabelle vengono archiviati nella stessa directory del sistema. Se l'origine dati è una directory di tabelle disponibile, il Driver ODBC Visual FoxPro non catalogo o restituire i nomi di tutte le tabelle che sono associati a un database.  
  
 Per altre informazioni, vedere [SQLTables](../../odbc/reference/syntax/sqltables-function.md) nel *riferimento per programmatori ODBC*.
