---
title: Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97224f53bb716abe3b79dd00df12d0eed4a63cec
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027846"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

In questo articolo vengono fornite informazioni sulle due modifiche implementate per migliorare le prestazioni del driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Invio in batch di istruzioni non preparate per le istruzioni preparate
Dalla versione 6.1.6-Preview, un miglioramento delle prestazioni è stato implementato grazie alla riduzione dei round trip del server a SQL Server. In precedenza, per ogni query prepareStatement è stata inviata anche una chiamata a Unprep. A questo punto, il driver esegue l'invio in batch di query di dispreparazione fino alla soglia "ServerPreparedStatementDiscardThreshold", che ha un valore predefinito di 10.

> [!NOTE]  
>  Gli utenti possono modificare il valore predefinito con il metodo seguente: setServerPreparedStatementDiscardThreshold (valore int)

Un'altra modifica introdotta da 6.1.6-Preview è che, prima di questa operazione, il driver chiamerebbe sempre sp_prepexec. A questo punto, per la prima esecuzione di un'istruzione preparata, il driver chiama sp_executesql e per il resto esegue sp_prepexec e assegna un handle. Altre informazioni sono disponibili [qui](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Gli utenti possono modificare il comportamento predefinito nelle versioni precedenti di chiamando sempre sp_prepexec impostando enablePrepareOnFirstPreparedStatementCall su **true** usando il metodo seguente: setEnablePrepareOnFirstPreparedStatementCall (valore booleano )

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Elenco delle nuove API introdotte con questa modifica, per l'invio in batch di istruzioni preparate per la preparazione

 **SQLServerConnection**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Restituisce il numero di operazioni preparate per l'istruzione Unprep attualmente in attesa.|
|void closeUnreferencedPreparedStatementHandles()|Impone l'esecuzione di richieste di annullamento della preparazione per eventuali istruzioni preparate scartate in attesa.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Restituisce il comportamento per un'istanza di connessione specifica. Se false la prima esecuzione chiama sp_executesql e non prepara un'istruzione, una volta eseguita la seconda esecuzione chiama sp_prepexec e imposta effettivamente un handle di istruzione preparato. Le esecuzioni seguenti chiamano sp_execute. Questa operazione elimina la necessità di sp_unprepare in caso di chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta. Il valore predefinito per questa opzione può essere modificato chiamando setDefaultEnablePrepareOnFirstPreparedStatementCall ().|
|void setEnablePrepareOnFirstPreparedStatementCall (valore booleano)|Specifica il comportamento per un'istanza di connessione specifica. Se value è false, la prima esecuzione chiama sp_executesql e non prepara un'istruzione, una volta eseguita la seconda esecuzione, chiama sp_prepexec e imposta effettivamente un handle di istruzione preparato. Le esecuzioni seguenti chiamano sp_execute. Questa operazione elimina la necessità di sp_unprepare in caso di chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.|
|int getServerPreparedStatementDiscardThreshold()|Restituisce il comportamento per un'istanza di connessione specifica. Questa impostazione consente di controllare il numero di azioni di eliminazione di istruzioni preparate (sp_unprepare) in attesa per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in attesa nel server. Se l'impostazione è < = 1, le azioni di unpreping vengono eseguite immediatamente dopo la chiusura dell'istruzione preparata. Se è impostato su {@literal >} 1, queste chiamate vengono raggruppate in batch per evitare un sovraccarico della chiamata di sp_unprepare troppo spesso. Il valore predefinito per questa opzione può essere modificato chiamando getDefaultServerPreparedStatementDiscardThreshold ().|
|void setServerPreparedStatementDiscardThreshold (valore int)|Specifica il comportamento per un'istanza di connessione specifica. Questa impostazione consente di controllare il numero di azioni di eliminazione di istruzioni preparate (sp_unprepare) in attesa per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in attesa nel server. Se l'impostazione è < = 1, le azioni non preparate vengono eseguite immediatamente in caso di chiusura dell'istruzione preparata. Se è impostato su > 1, queste chiamate vengono raggruppate in batch per evitare un sovraccarico della chiamata di sp_unprepare troppo spesso.|

 **SQLServerDataSource**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall (Boolean enablePrepareOnFirstPreparedStatementCall)|Se questa configurazione è false, la prima esecuzione di un'istruzione preparata chiama sp_executesql e non prepara un'istruzione, una volta eseguita la seconda esecuzione, chiama sp_prepexec e imposta effettivamente un handle di istruzione preparato. Le esecuzioni seguenti chiamano sp_execute. Questa operazione elimina la necessità di sp_unprepare in caso di chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Se questa configurazione restituisce false la prima esecuzione di un'istruzione preparata chiama sp_executesql e non prepara un'istruzione, una volta eseguita la seconda esecuzione, chiama sp_prepexec e imposta effettivamente un handle di istruzione preparato. Le esecuzioni seguenti chiamano sp_execute. Questa operazione elimina la necessità di sp_unprepare in caso di chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.|
|void setServerPreparedStatementDiscardThreshold (int serverPreparedStatementDiscardThreshold)|Questa impostazione consente di controllare il numero di azioni di eliminazione di istruzioni preparate (sp_unprepare) in attesa per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in attesa nel server. Se l'impostazione è < = 1, le azioni non preparate vengono eseguite immediatamente in caso di chiusura dell'istruzione preparata. Se è impostato su {@literal >} 1, queste chiamate vengono raggruppate in batch per evitare un sovraccarico della chiamata di sp_unprepare troppo spesso|
|int getServerPreparedStatementDiscardThreshold()|Questa impostazione consente di controllare il numero di azioni di eliminazione di istruzioni preparate (sp_unprepare) in attesa per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in attesa nel server. Se l'impostazione è < = 1, le azioni non preparate vengono eseguite immediatamente in caso di chiusura dell'istruzione preparata. Se è impostato su {@literal >} 1, queste chiamate vengono raggruppate in batch per evitare un sovraccarico della chiamata di sp_unprepare troppo spesso.|

## <a name="prepared-statement-metatada-caching"></a>Metadati di istruzioni preparate Caching
A partire da 6.3.0-versione di anteprima, Microsoft JDBC Driver for SQL Server supporta la memorizzazione nella cache di istruzioni preparate. Prima di v 6.3.0-Preview, se si esegue una query che è già stata preparata e archiviata nella cache, la chiamata della stessa query non comporterà la preparazione. A questo punto, il driver cerca la query nella cache e trova il punto di manipolazione e lo esegue con sp_execute.
La memorizzazione nella cache dei metadati dell'istruzione preparata è **disabilitata** per impostazione predefinita. Per abilitarla, è necessario chiamare il metodo seguente nell'oggetto Connection:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Ad esempio: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Elenco delle nuove API introdotte con questa modifica, per la memorizzazione nella cache dei metadati dell'istruzione preparata

 **SQLServerConnection**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|void setDisableStatementPooling (valore booleano)|Imposta il pool di istruzioni su true o false.|
|boolean getDisableStatementPooling()|Restituisce true se il pool di istruzioni è disabilitato.|
|void setStatementPoolingCacheSize(int value)|Specifica le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore minore di 1 indica nessuna cache.|
|int getStatementPoolingCacheSize()|Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore minore di 1 indica nessuna cache.|
|int getStatementHandleCacheEntryCount()|Restituisce il numero corrente di handle di istruzione preparati in pool.|
|boolean isPreparedStatementCachingEnabled()|Indica se il pool di istruzioni è abilitato o meno per questa connessione.|

 **SQLServerDataSource**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|void setDisableStatementPooling (Boolean disableStatementPooling)|Imposta il pool di istruzioni su true o false|
|boolean getDisableStatementPooling()|Restituisce true se il pool di istruzioni è disabilitato.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Specifica le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore minore di 1 indica nessuna cache.|
|int getStatementPoolingCacheSize()|Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore minore di 1 indica nessuna cache.|

## <a name="see-also"></a>Vedere anche  
 [Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
