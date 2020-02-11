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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88edec63a97ff6c463f07add895ff8399fc4268a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046756"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  Per le istruzioni eseguite, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC di Native client non visita il server per segnalare il numero di colonne in un set di risultati. In questo caso, `SQLNumResultCols` non causa un round trip del server. Analogamente a [](sqlcolattribute.md) [SQLDescribeCol](sqldescribecol.md) e SQLColAttribute `SQLNumResultCols` , la chiamata a istruzioni preparate ma non eseguite genera un round trip del server.  
  
 Quando un'istruzione o un batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] restituisce più set di righe di risultati, è possibile che il numero di colonne del set di risultati cambi da un set all'altro. `SQLNumResultCols`deve essere chiamato per ogni set. Quando il numero di colonne cambia, l'applicazione deve riassociare i valori dei dati prima di recuperare i risultati delle righe. Per ulteriori informazioni sulla gestione di più restituzione di set di risultati, vedere [SQLMoreResults](sqlmoreresults.md).  
  
 I miglioramenti apportati al motore [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di database a partire da consentono a SQLNumResultCols di ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati possono essere diversi dai valori restituiti da SQLNumResultCols nelle versioni precedenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLNumResultCols (funzione)](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
