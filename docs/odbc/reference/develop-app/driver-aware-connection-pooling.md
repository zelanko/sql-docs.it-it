---
description: Pool di connessioni compatibile con il driver
title: Pool di connessioni compatibile con il driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed2fa29a68095be9cfcc7d4192c6dc2e15f3eac7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494659"
---
# <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver
Il pool di connessioni compatibile con il driver è una nuova funzionalità di gestione driver in Windows 8. Il pool di connessioni compatibile con il driver consente ai writer di driver di personalizzare il comportamento del pool di connessioni nel driver ODBC.  
  
> [!NOTE]  
>  Il pool di connessioni compatibile con il driver non è supportato con la libreria di cursori. Un'applicazione riceverà un messaggio di errore se tenta di abilitare la libreria di cursori tramite SQLSetConnectAttr, quando il pool di connessioni compatibile con il driver è abilitato.  
  
 Il pool di connessioni compatibile con il driver risolve i problemi seguenti relativi al pool di connessioni di gestione driver:  
  
 **Frammentazione del pool** Gestione driver restituirà solo una connessione dal pool se corrisponde esattamente alla stringa di connessione di una nuova richiesta di connessione.  Un motivo per cui gestione driver richiede una corrispondenza esatta è che Gestione driver non comprende tutte le parole chiave della stringa di connessione specifiche del driver e il relativo valore.  Tuttavia, alcuni valori di parole chiave della stringa di connessione, ad esempio il nome del database, potrebbero non richiedere una corrispondenza esatta, perché il driver può modificare il database in meno del tempo necessario per aprire una nuova connessione (la differenza di tempo esatta dipende dall'origine dati). E, le differenze in alcuni attributi di connessione (ad esempio SQL_ATTR_CURRENT_CATALOG) possono richiedere più tempo rispetto alle differenze in altri attributi, ad esempio SQL_ATTR_LOGIN_TIMEOUT. Questo, inoltre, può impedire a gestione driver di usare la connessione riutilizzabile a costo inferiore dal pool. Quando un driver deve creare numerose nuove connessioni, le prestazioni di un'applicazione possono ridursi e la scalabilità dell'origine dati può ridursi. La frammentazione del pool può essere ridotta con il pool di connessioni compatibile con il driver perché un driver può stimare meglio il costo di riutilizzo di una connessione nel pool per una richiesta di connessione.  
  
 **Nessuna considerazione della preferenza dell'applicazione** Alcune origini dati possono aprire in modo efficiente nuove connessioni (rispetto alla reimpostazione di alcuni attributi). in questo modo, un'applicazione potrebbe preferire l'apertura di una nuova connessione anziché il tentativo di riutilizzare una connessione leggermente non corrispondente dal pool e di reimpostare alcuni valori (sebbene questo potrebbe risultare più lento durante la frase di inizializzazione del pool di connessioni). Tuttavia, alcune applicazioni possono ridurre il carico del server e aprire un minor numero di connessioni, anche se è possibile che si verifichi un costo maggiore per correggere le mancate corrispondenze per un comportamento corretto. Senza il pool di connessioni compatibile con il driver, non è possibile specificare in modo efficace questo tipo di preferenza, perché Gestione driver non riconosce tutti gli attributi di connessione specifici del driver. Il pool di connessioni compatibile con il driver consente a un driver di ottenere la preferenza dell'utente (con un attributo specifico del driver SQLSetConnectAttr), in modo da poter stimare meglio il costo del riutilizzo di una connessione dal pool in base alle preferenze dell'utente.  
  
 Per ulteriori informazioni sul pool di connessioni compatibile con il driver, vedere [sviluppo della conoscenza del pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinazione del supporto driver  
 Il pool di connessioni compatibile con il driver è una funzionalità facoltativa che un driver potrebbe non supportare. Per determinare se un driver lo supporta, usare il SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* di [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Come abilitare il pool di connessioni compatibile con il driver  
 Un'applicazione può utilizzare la consapevolezza del pool di connessioni di un driver impostando l'attributo SQL_ATTR_CONNECTION_POOLING su SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se un driver non supporta la consapevolezza del pool di connessioni, verrà utilizzato il pool di connessioni di gestione driver (come se fosse stato specificato SQL_CP_ONE_PER_HENV, anziché SQL_CP_DRIVER_AWARE). Le applicazioni ODBC 2. x e 3. x possono abilitare questa funzionalità.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
