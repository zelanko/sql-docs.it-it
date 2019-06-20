---
title: Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 58ebcb2560e3b03703d7a419b28c6c04e41c19f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794090"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo fornisce informazioni sulle due modifiche implementate per migliorare le prestazioni del driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Invio in batch di Unprepare per le istruzioni preparate
Poiché 6.1.6-preview versione, un miglioramento delle prestazioni è stata implementata tramite riducendo al minimo server round trip a SQL Server. In precedenza, per ogni query prepareStatement, una chiamata a unprepare è stata inviata anche. A questo punto, il driver è batch unprepare query fino a "ServerPreparedStatementDiscardThreshold", che ha un valore predefinito di 10 la soglia.

> [!NOTE]  
>  Gli utenti possono modificare il valore predefinito con il metodo seguente: setServerPreparedStatementDiscardThreshold (valore int)

Un'altra modifica introdotta da 6.1.6-preview è che prima di questa driver sempre chiamerebbe sp_prepexec. A questo punto, per la prima esecuzione di un'istruzione preparata, il driver chiama sp_executesql e per il resto esegue sp_prepexec e assegna un handle a esso. Altre informazioni sono reperibili [qui](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Gli utenti possono modificare il comportamento predefinito per le versioni precedenti di chiamare sempre sp_prepexec dall'impostazione enablePrepareOnFirstPreparedStatementCall al **true** usando il metodo seguente: setEnablePrepareOnFirstPreparedStatementCall (valore booleano)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Elenco delle nuove API introdotte con questa modifica, per l'invio in batch di Unprepare per le istruzioni preparate

 **SQLServerConnection**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Restituisce il numero di attualmente in sospeso preparata istruzione unprepare azioni.|
|closeUnreferencedPreparedStatementHandles() void|Forza le richieste unprepare per qualsiasi istruzione preparate scartati in sospeso da eseguire.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Restituisce il comportamento per un'istanza di connessione specifica. Se false la prima esecuzione chiama sp_executesql e non preparare un'istruzione, dopo l'esecuzione secondo avviene chiama sp_prepexec ed effettivamente configurare un handle di istruzione preparata. Sp_execute chiamate esecuzioni seguito. Ciò riduce la necessità per sp_unprepare in istruzione preparata chiudere se l'istruzione viene eseguita solo una volta. Il valore predefinito per questa opzione può essere modificato da setDefaultEnablePrepareOnFirstPreparedStatementCall() chiamante.|
|setEnablePrepareOnFirstPreparedStatementCall(boolean value) void|Specifica il comportamento per un'istanza di connessione specifica. Se il valore è false la prima esecuzione chiama sp_executesql e non preparare un'istruzione, dopo l'esecuzione secondo avviene chiama sp_prepexec ed effettivamente configurare un handle di istruzione preparata. Sp_execute chiamate esecuzioni seguito. Ciò riduce la necessità per sp_unprepare in istruzione preparata chiudere se l'istruzione viene eseguita solo una volta.|
|int getServerPreparedStatementDiscardThreshold()|Restituisce il comportamento per un'istanza di connessione specifica. Questa impostazione Controlla quanti preparato in sospeso variabile discard istruzione azioni (sp_unprepare) possono rimanere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Se l'impostazione è < = 1, unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se è impostato su {@literal >} 1, queste chiamate vengono eseguite in batch insieme per evitare sovraccarichi del chiamante sp_unprepare troppo spesso. Il valore predefinito per questa opzione può essere modificato da getDefaultServerPreparedStatementDiscardThreshold() chiamante.|
|setServerPreparedStatementDiscardThreshold(int value) void|Specifica il comportamento per un'istanza di connessione specifica. Questa impostazione Controlla quanti preparato in sospeso variabile discard istruzione azioni (sp_unprepare) possono rimanere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Se l'impostazione è < = 1 unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se è impostato su 1 > queste chiamate vengono eseguite in batch insieme per evitare il sovraccarico della chiamata al metodo sp_unprepare troppo spesso.|

 **SQLServerDataSource**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall) void|Se questa configurazione è false la prima esecuzione di un'istruzione preparata chiama sp_executesql e non preparare un'istruzione, dopo l'esecuzione secondo avviene chiama sp_prepexec ed effettivamente configurare un handle di istruzione preparata. Sp_execute chiamate esecuzioni seguito. Ciò riduce la necessità per sp_unprepare in istruzione preparata chiudere se l'istruzione viene eseguita solo una volta.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Se questa configurazione restituirà false la prima esecuzione di un'istruzione preparata chiama sp_executesql e non prepara un'istruzione, una volta la seconda esecuzione si verifica, chiama sp_prepexec ed effettivamente impostare un handle di istruzione preparata. Sp_execute chiamate esecuzioni seguito. Ciò riduce la necessità per sp_unprepare in istruzione preparata chiudere se l'istruzione viene eseguita solo una volta.|
|setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold) void|Questa impostazione Controlla quanti preparato in sospeso variabile discard istruzione azioni (sp_unprepare) possono rimanere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Se l'impostazione è < = 1 unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se è impostato su {@literal >} 1 vengono eseguite in batch insieme queste chiamate per evitare il sovraccarico della chiamata al metodo sp_unprepare troppo spesso|
|int getServerPreparedStatementDiscardThreshold()|Questa impostazione Controlla quanti preparato in sospeso variabile discard istruzione azioni (sp_unprepare) possono rimanere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Se l'impostazione è < = 1 unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se è impostato su {@literal >} 1 vengono eseguite in batch insieme queste chiamate per evitare il sovraccarico della chiamata al metodo sp_unprepare troppo spesso.|

## <a name="prepared-statement-metatada-caching"></a>Memorizzazione nella cache i metadati di istruzione preparata
A partire dalla versione 6.3.0-preview, Microsoft JDBC driver per SQL Server supporta la memorizzazione nella cache di un'istruzione preparata. Prima di v6.3.0-preview, se uno esegue una query che è stata già preparata e archiviata nella cache, chiamando di nuovo la stessa query non comporterà la preparazione. A questo punto, il driver cerca la query nella cache e trovare l'handle ed eseguirlo con sp_execute.
Memorizzazione nella cache dei metadati di istruzione preparata viene **disabilitato** per impostazione predefinita. Per abilitarla, è necessario chiamare il metodo seguente sull'oggetto connessione:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Ad esempio: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Elenco delle nuove API introdotte con questa modifica, per un'istruzione preparata la memorizzazione nella cache dei metadati

 **SQLServerConnection**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|setDisableStatementPooling(boolean value) void|Imposta il pool di istruzioni su true o false.|
|getDisableStatementPooling() booleano|Restituisce true se il pool di istruzioni è disabilitato.|
|void setStatementPoolingCacheSize(int value)|Specifica le dimensioni della cache dell'istruzione preparata per la connessione. Un valore minore di 1 non significa Nessuna cache.|
|int getStatementPoolingCacheSize()|Restituisce le dimensioni della cache dell'istruzione preparata per la connessione. Un valore minore di 1 non significa Nessuna cache.|
|int getStatementHandleCacheEntryCount()|Restituisce il numero corrente di handle di istruzione preparata in pool.|
|boolean isPreparedStatementCachingEnabled()|Se l'istruzione di limitazione delle richieste è abilitata o meno per questa connessione.|

 **SQLServerDataSource**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|setDisableStatementPooling(boolean disableStatementPooling) void|Imposta l'istruzione di limitazione delle richieste su true o false|
|getDisableStatementPooling() booleano|Restituisce true se il pool di istruzioni è disabilitato.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Specifica le dimensioni della cache dell'istruzione preparata per la connessione. Un valore minore di 1 non significa Nessuna cache.|
|int getStatementPoolingCacheSize()|Restituisce le dimensioni della cache dell'istruzione preparata per la connessione. Un valore minore di 1 non significa Nessuna cache.|

## <a name="see-also"></a>Vedere anche  
 [Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
