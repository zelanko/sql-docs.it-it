---
title: Messaggi di errore | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b38734544ac3accb3ddfdbcae8ae92f67b252e54
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805855"
---
# <a name="error-messages"></a>messaggi di errore
  Il testo dei messaggi restituiti dal driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC di Native client viene inserito nel parametro *MessageText* di **SQLGetDiagRec**. L'origine di un errore viene indicata dall'intestazione del messaggio:  
  
 [Microsoft][Gestione driver ODBC]  
 Questi errori vengono generati da Gestione driver ODBC.  
  
 [Microsoft][Libreria di cursori ODBC]  
 Questi errori vengono generati dalla libreria di cursori ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Questi errori vengono generati dal driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC di Native Client. Se non sono presenti altri nodi con il nome di una libreria di rete o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'errore è stato rilevato nel driver.  
  
 Microsoft [SQL Server Native Client] [*Net-transportaname*]  
 Questi errori vengono generati dalla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libreria di rete, dove *net-TransportName* è il nome visualizzato del trasporto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rete di un client, ad esempio Named Pipes, Shared Memory, TCP/IP Sockets o via. Il resto del messaggio di errore contiene la funzione della libreria di rete chiamata e la funzione chiamata nell'API di rete sottostante dalla funzione TDS. Il codice di errore *pfNative* restituito con questi errori è il codice di errore dello stack del protocollo di rete sottostante.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 Questi errori vengono generati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il resto del messaggio di errore corrisponde al testo del messaggio di errore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il codice *pfNative* restituito con questi errori è il numero di errore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Per ulteriori informazioni su un elenco di messaggi di errore (e sui relativi numeri) che possono essere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]restituiti da, vedere la descrizione e le colonne di errore della tabella di sistema **sysmessages** nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database **Master** in.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione di errori e messaggi](handling-errors-and-messages.md)  
  
  
