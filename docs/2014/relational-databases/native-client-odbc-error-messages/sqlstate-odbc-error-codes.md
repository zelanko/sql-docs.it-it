---
title: SQLSTATE (codici di errore ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: rothja
ms.author: jroth
ms.openlocfilehash: ff3ec0a5cdc8f24f34e42849f7c8f6d1d9d41478
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019912"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (codici di errore ODBC)
  SQLSTATE fornisce informazioni dettagliate sulla causa di un avviso o di un errore. Per gli errori che si verificano nell'origine dati rilevata e restituita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client esegue il mapping del numero di errore nativo restituito all'SQLSTATE appropriato. Se un numero di errore nativo non dispone di un codice di errore ODBC a cui eseguire il mapping, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client restituisce SQLSTATE 42000 ("errore di sintassi o violazione di accesso"). Per gli errori rilevati dal driver, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client genera il SQLSTATE appropriato.  
  
 Per ulteriori informazioni sui codici di errore di stato, vedere i seguenti argomenti:  
  
-   [Appendice A: codici di errore ODBC](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Mapping di SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](handling-errors-and-messages.md)  
  
  
