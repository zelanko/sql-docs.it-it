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
author: rothja
ms.author: jroth
ms.openlocfilehash: d004ba320b50896b6f57c5de335d7f7b3d33e87a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020043"
---
# <a name="error-messages"></a>messaggi di errore
  Il testo dei messaggi restituiti dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client viene inserito nel parametro *MessageText* di **SQLGetDiagRec**. L'origine di un errore viene indicata dall'intestazione del messaggio:  
  
 [Microsoft][Gestione driver ODBC]  
 Questi errori vengono generati da Gestione driver ODBC.  
  
 [Microsoft][Libreria di cursori ODBC]  
 Questi errori vengono generati dalla libreria di cursori ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Questi errori vengono generati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client. Se non sono presenti altri nodi con il nome di una libreria di rete o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'errore è stato rilevato nel driver.  
  
 Microsoft [SQL Server Native Client] [*Net-transportaname*]  
 Questi errori vengono generati dalla libreria di rete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , dove *net-TransportName* è il nome visualizzato del trasporto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rete di un client, ad esempio Named Pipes, Shared Memory, TCP/IP Sockets o via. Il resto del messaggio di errore contiene la funzione della libreria di rete chiamata e la funzione chiamata nell'API di rete sottostante dalla funzione TDS. Il codice di errore *pfNative* restituito con questi errori è il codice di errore dello stack del protocollo di rete sottostante.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 Questi errori vengono generati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il resto del messaggio di errore corrisponde al testo del messaggio di errore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il codice *pfNative* restituito con questi errori è il numero di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ulteriori informazioni su un elenco di messaggi di errore (e sui relativi numeri) che possono essere restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere la descrizione e le colonne di errore della tabella di sistema **sysmessages** nel database **Master** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](handling-errors-and-messages.md)  
  
  
