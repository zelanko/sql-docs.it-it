---
title: Pool di connessioni compatibile con il driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dee7ee2b08e4b3b0249ede7f999cfb23d8db944
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047051"
---
# <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver
Il pool di connessioni compatibile con il driver è una nuova funzionalità di gestione Driver in Windows 8. Il pool di connessioni compatibile con il driver consente ai writer di driver di personalizzare il comportamento nel loro driver ODBC di pool di connessioni.  
  
> [!NOTE]  
>  Il pool di connessioni compatibile con il driver non è supportato con libreria di cursori. Un'applicazione verrà visualizzato il messaggio di errore se tenta di abilitare la libreria di cursori tramite SQLSetConnectAttr, quando il pool di connessioni compatibile con il driver è abilitato.  
  
 Il pool di indirizzi di connessioni compatibile con driver i seguenti problemi correlati al pool di connessioni di gestione Driver:  
  
 **Frammentazione del pool** The Driver Manager restituirà solo una connessione dal pool se è una corrispondenza esatta con la stringa di connessione di una nuova richiesta di connessione.  Uno dei motivi per la gestione Driver per richiedere una corrispondenza esatta è che Gestione Driver non riconosce qualsiasi parola chiave stringa di connessione specifici del driver e il relativo valore.  Tuttavia, alcuni valori di parola chiave di stringa di connessione (ad esempio il nome del database) non richiedano una corrispondenza esatta, poiché il driver può modificare il database in meno rispetto al tempo necessario per aprire una nuova connessione (la differenza di ora esatta dipende dall'origine dati). E le differenze di alcuni attributi di connessione (ad esempio SQL_ATTR_CURRENT_CATALOG) possono richiedere più tempo per modificare più le differenze negli altri attributi (ad esempio SQL_ATTR_LOGIN_TIMEOUT). Questo, troppo, può impedire la gestione di Driver utilizzando la connessione a costo più basso e riutilizzabile dal pool. Quando si dispone di un driver creare molte nuove connessioni, possano riduzione delle prestazioni di un'applicazione e può ridurre la scalabilità di origine dati. È possibile ridurre la frammentazione di pool con pool di connessioni compatibile con il driver perché un driver può stimare al meglio il costo di riutilizzare una connessione in pool per una richiesta di connessione.  
  
 **Nessuna preferenza applicazione tenendo in considerazione** alcune origini dati in modo efficiente possono aprire nuove connessioni (rispetto alla reimpostazione alcuni attributi), pertanto, un'applicazione potrebbe preferire aprire una nuova connessione invece di tentare di riutilizzare un leggermente non corrispondenti connessione dal pool e reimpostazione alcuni valori (anche se ciò può essere più lento durante la frase di inizializzazione del pool di connessione). Tuttavia, alcune applicazioni possono mantenere il carico del server più piccoli e aprire meno connessioni, anche se potrebbe esserci un costo maggiore per correggere le mancate corrispondenze per il comportamento corretto. Senza il pool di connessioni compatibile con il driver, è possibile specificare questo tipo di preferenza in modo efficace, perché Gestione Driver non riconosce tutti gli attributi di connessione specifici del driver. Pool di connessioni compatibile con il driver consente al driver ottenere le preferenze dell'utente (con un attributo specifico del driver di SQLSetConnectAttr) in modo che possono stimare al meglio il costo di riutilizzare una connessione dal pool in base alle preferenze dell'utente.  
  
 Per altre informazioni sui pool di connessioni compatibile con il driver, vedere [lo sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinare il supporto dei Driver  
 Pool di connessioni compatibile con il driver è una funzionalità facoltativa che non supportano un driver. Per determinare se un driver lo supporta, utilizzare il SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* dei [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Come abilitare il pool di connessioni compatibile con il Driver  
 Un'applicazione può usare il riconoscimento di pool di connessioni del driver impostando l'attributo SQL_ATTR_CONNECTION_POOLING su SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se un driver non supporta la consapevolezza di pool di connessioni, il pool di connessioni di gestione Driver verrà utilizzato (stesso come se fosse stato specificato SQL_CP_ONE_PER_HENV, anziché SQL_CP_DRIVER_AWARE). Le applicazioni ODBC 2.x e 3.x possono abilitare questa funzionalità.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
