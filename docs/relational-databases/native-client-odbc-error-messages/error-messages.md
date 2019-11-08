---
title: Messaggi di errore | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 10308509004493ba68d23870a70bf878ae05b4a1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783463"
---
# <a name="error-messages"></a>messaggi di errore
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il testo dei messaggi restituiti dal driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client viene inserito nel parametro *MessageText* di **SQLGetDiagRec**. L'origine di un errore viene indicata dall'intestazione del messaggio:  
  
 [Microsoft][Gestione driver ODBC]  
 Questi errori vengono generati da Gestione driver ODBC.  
  
 [Microsoft][Libreria di cursori ODBC]  
 Questi errori vengono generati dalla libreria di cursori ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Questi errori vengono generati dal driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Se non sono presenti altri nodi con il nome di una libreria di rete o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'errore è stato rilevato nel driver.  
  
 Microsoft [SQL Server Native Client] [*Net-transportaname*]  
 Questi errori vengono generati dalla libreria di rete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dove *net-transportaname* è il nome visualizzato di un trasporto di rete del client di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio named pipe, Shared Memory, TCP/IP Sockets o via. Il resto del messaggio di errore contiene la funzione della libreria di rete chiamata e la funzione chiamata nell'API di rete sottostante dalla funzione TDS. Il codice di errore *pfNative* restituito con questi errori è il codice di errore dello stack del protocollo di rete sottostante.  
  
 Microsoft [SQL Server Native Client] [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 Questi errori vengono generati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il resto del messaggio di errore corrisponde al testo del messaggio di errore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il codice *pfNative* restituito con questi errori è il numero di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni su un elenco di messaggi di errore (e sui relativi numeri) che possono essere restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la descrizione e le colonne di errore della tabella di sistema **sysmessages** nel database **Master** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
