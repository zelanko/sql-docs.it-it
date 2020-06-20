---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: rothja
ms.author: jroth
ms.openlocfilehash: 45e72165eef621dc377b02ed3d2e7e1e3cf7ab8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021868"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  Per le istruzioni eseguite, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client non visita il server per segnalare il numero di colonne in un set di risultati. In questo caso, non `SQLNumResultCols` causa un round trip del server. Analogamente a [SQLDescribeCol](sqldescribecol.md) e [SQLColAttribute](sqlcolattribute.md), `SQLNumResultCols` la chiamata a istruzioni preparate ma non eseguite genera un round trip del server.  
  
 Quando un'istruzione o un batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] restituisce più set di righe di risultati, è possibile che il numero di colonne del set di risultati cambi da un set all'altro. `SQLNumResultCols`deve essere chiamato per ogni set. Quando il numero di colonne cambia, l'applicazione deve riassociare i valori dei dati prima di recuperare i risultati delle righe. Per ulteriori informazioni sulla gestione di più restituzione di set di risultati, vedere [SQLMoreResults](sqlmoreresults.md).  
  
 I miglioramenti apportati al motore di database a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] consentono a SQLNumResultCols di ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati possono essere diversi dai valori restituiti da SQLNumResultCols nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLNumResultCols (funzione)](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
