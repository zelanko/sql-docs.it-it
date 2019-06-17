---
title: SQLExtendedFetch (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2d01c25044bf7b03e2fabe9c615668fc7837312
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313247"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 2  
  
 Simile a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ma restituisce più righe utilizzando una matrice per ogni colonna. Il set di risultati forward-supporta lo scorrimento e può essere eseguito con le versioni precedenti-scorrevole se il cursore viene definito come static e non forward-only.  
  
 Per impostazione predefinita, il Driver ODBC Visual FoxPro non restituisce righe contrassegnate come eliminate in una tabella FoxPro. Le righe contrassegnate per l'eliminazione ma non ancora rimossi da una tabella non sono inclusi nel cursore del set di risultati. È possibile modificare questo comportamento usando il [SET DELETED](../../odbc/microsoft/set-deleted-command.md) comando.  
  
 Per altre informazioni, vedere [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) nel *riferimento per programmatori ODBC*.
