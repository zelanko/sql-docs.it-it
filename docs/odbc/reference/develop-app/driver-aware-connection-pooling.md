---
title: Pool di connessioni in grado di riconoscere il driver Documenti Microsoft
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
ms.openlocfilehash: 70b70c841f37bd69179137c807c0dadcfd932d2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287601"
---
# <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver
Il pool di connessioni in grado di riconoscere i driver è una nuova funzionalità di Gestione Driver in Windows 8. Il pool di connessioni in grado di riconoscere i driver consente agli autori di driver di personalizzare il comportamento del pool di connessioni nel driver ODBC.  
  
> [!NOTE]  
>  Il pool di connessioni in grado di riconoscere i driver non è supportato con la libreria di cursori. Un'applicazione riceverà un messaggio di errore se tenta di abilitare la libreria di cursori tramite SQLSetConnectAttr, quando il pool di connessioni in grado di riconoscere i driver è abilitato.  
  
 Il pool di connessioni in grado di riconoscere driver risolve i problemi seguenti relativi al pool di connessioni di Gestione Driver:  
  
 **Frammentazione del poolPool Fragmentation** Gestione Driver restituirà una connessione dal pool solo se si tratta di una corrispondenza esatta con la stringa di connessione di una nuova richiesta di connessione.  Uno dei motivi per cui Gestione Driver richiede una corrispondenza esatta è che Gestione Driver non riconosce ogni parola chiave stringa di connessione specifica del driver e il relativo valore.  Tuttavia, alcuni valori di parola chiave della stringa di connessione (ad esempio il nome del database) potrebbero non richiedere una corrispondenza esatta, poiché il driver può modificare il database in meno del tempo necessario per aprire una nuova connessione (la differenza di ora esatta dipende dall'origine dati). Inoltre, le differenze in alcuni attributi di connessione (ad esempio SQL_ATTR_CURRENT_CATALOG) possono richiedere più tempo per la modifica rispetto alle differenze in altri attributi (ad esempio SQL_ATTR_LOGIN_TIMEOUT). Anche questo può impedire a Gestione Driver di utilizzare la connessione riutilizzabile più economica dal pool. Quando un driver deve creare molte nuove connessioni, le prestazioni di un'applicazione possono diminuire e la scalabilità dell'origine dati può diminuire. La frammentazione del pool può essere ridotta con il pool di connessioni in grado di riconoscere i driver perché un driver può stimare meglio il costo del riutilizzo di una connessione nel pool per una richiesta di connessione.  
  
 **Nessuna considerazione della preferenza dell'applicazione** Alcune origini dati possono aprire in modo efficiente nuove connessioni (rispetto alla reimpostazione di alcuni attributi), pertanto un'applicazione potrebbe preferire aprire una nuova connessione anziché tentare di riutilizzare una connessione leggermente non corrispondente dal pool e reimpostare alcuni valori (anche se questo potrebbe essere più lento durante la frase di inizializzazione del pool di connessioni). Ma alcune applicazioni possono mantenere il carico del server più piccolo e aprire meno connessioni, anche se ci può essere un costo maggiore per risolvere le mancate corrispondenze per il comportamento corretto. Senza il pool di connessioni in grado di riconoscere i driver, non è possibile specificare questo tipo di preferenza in modo efficace, perché Gestione Driver non riconosce tutti gli attributi di connessione specifici del driver. Il pool di connessioni in grado di riconoscere i driver consente a un driver di ottenere le preferenze utente (con un attributo specifico del driver di SQLSetConnectAttr) in modo da poter stimare meglio il costo del riutilizzo di una connessione dal pool in base alle preferenze dell'utente.  
  
 Per ulteriori informazioni sul pool di connessioni in grado di riconoscere i driver, vedere [Sviluppo del riconoscimento](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)del pool di connessioni in un driver ODBC .  
  
## <a name="determining-driver-support"></a>Determinazione del supporto del driver  
 Il pool di connessioni in grado di riconoscere il driver è una funzionalità facoltativa che un driver potrebbe non supportare. Per determinare se un driver lo supporta, utilizzare il SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* di [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Abilitazione del pool di connessioni in grado di riconoscere i driver  
 Un'applicazione può utilizzare il riconoscimento del pool di connessioni di un driver impostando l'attributo SQL_ATTR_CONNECTION_POOLING su SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se un driver non supporta il riconoscimento del pool di connessioni, verrà utilizzato il pool di connessioni di Gestione Driver (come se fosse stato specificato SQL_CP_ONE_PER_HENV, anziché SQL_CP_DRIVER_AWARE). Le applicazioni ODBC 2.x e 3.x possono abilitare questa funzionalità.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
