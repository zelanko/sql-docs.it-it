---
title: Esecuzione delle transazioni distribuite | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa5c6b607fa7523380950ecd89f9cae20ffc6f21
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228956"
---
# <a name="performing-distributed-transactions"></a>Esecuzione delle transazioni distribuite
  Microsoft Distributed Transaction Coordinator (MS DTC) consente alle applicazioni di estendere le transazioni su due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], nonché di partecipare a transazioni gestite da gestori transazioni conformi allo standard DTP XA dell'Open Group.  
  
 In genere tutti i comandi di gestione delle transazioni vengono inviati al server tramite il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. L'applicazione avvia una transazione chiamando [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) con la modalità autocommit disabilitata. Esegue quindi gli aggiornamenti che comprendono la transazione e chiama [SQLEndTran](../../native-client-odbc-api/sqlendtran.md) con l'opzione SQL_COMMIT o SQL_ROLLBACK.  
  
 Quando si utilizza MS DTC, tuttavia, MS DTC diventa il gestore delle transazioni e l'applicazione non vengono più utilizzati **SQLEndTran**.  
  
 Dopo aver eseguito l'integrazione in una transazione distribuita e, successivamente, aver effettuato la stessa operazione in una seconda transazione distribuita, il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene escluso dalla transazione distribuita originale e ne viene eseguita l'integrazione nella nuova transazione. Per altre informazioni, vedere [di riferimento per programmatori di DTC](https://msdn.microsoft.com/library/ms686108\(VS.85\).aspx).  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di transazioni di &#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
