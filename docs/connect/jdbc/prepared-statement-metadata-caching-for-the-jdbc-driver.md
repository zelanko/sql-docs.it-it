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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027846"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo contiene informazioni sulle due modifiche implementate per migliorare le prestazioni del driver.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Invio in batch dell'annullamento della preparazione per le istruzioni preparate
A partire dalla versione 6.1.6-anteprima, è stato implementato un miglioramento delle prestazioni tramite la riduzione dei round trip del server a SQL Server. In precedenza, per ogni query prepareStatement veniva inviata anche una chiamata per l'annullamento della preparazione. Ora il driver esegue l'invio in batch delle query di annullamento della preparazione fino alla soglia "ServerPreparedStatementDiscardThreshold", che ha un valore predefinito di 10.

> [!NOTE]  
>  Gli utenti possono modificare il valore predefinito con il metodo seguente: setServerPreparedStatementDiscardThreshold(int value)

Un'altra modifica introdotta a partire dalla versione 6.1.6-anteprima è che in precedenza il driver chiamava sempre sp_prepexec. Per la prima esecuzione di un'istruzione preparata, ora il driver chiama sp_executesql e per il resto esegue sp_prepexec e vi assegna un handle. Per informazioni dettagliate, vedere [questo articolo](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Gli utenti possono modificare il comportamento predefinito delle versioni precedenti che chiamavano sempre sp_prepexec impostando enablePrepareOnFirstPreparedStatementCall su **true** tramite il metodo seguente: setEnablePrepareOnFirstPreparedStatementCall(boolean value)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Elenco delle nuove API introdotte con questa modifica, per l'invio in batch dell'annullamento della preparazione per le istruzioni preparate

 **SQLServerConnection**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Restituisce il numero di azioni di annullamento della preparazione per le istruzioni preparate attualmente in attesa.|
|void closeUnreferencedPreparedStatementHandles()|Impone richieste di annullamento della preparazione per eventuali istruzioni preparate per l'esecuzione e rimosse in sospeso.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Restituisce il comportamento per un'istanza di connessione specifica. Se il valore è false, la prima esecuzione chiama sp_executesql e non prepara un'istruzione. La seconda esecuzione chiama sp_prepexec e imposta effettivamente un handle per l'istruzione preparata. Le esecuzioni seguenti chiamano sp_execute. Viene così eliminata la necessità di sp_unprepare alla chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta. L'impostazione predefinita per questa opzione può essere modificata chiamando setDefaultEnablePrepareOnFirstPreparedStatementCall().|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Specifica il comportamento per un'istanza di connessione specifica. Se il valore è false, la prima esecuzione chiama sp_executesql e non prepara un'istruzione. La seconda esecuzione chiama sp_prepexec e imposta effettivamente un handle per l'istruzione preparata. Le esecuzioni seguenti chiamano sp_execute. Viene così eliminata la necessità di sp_unprepare alla chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.|
|int getServerPreparedStatementDiscardThreshold()|Restituisce il comportamento per un'istanza di connessione specifica. Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Se l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se è impostata su {@literal >} 1, queste chiamate vengono raggruppate per evitare un sovraccarico troppo frequente della chiamata di sp_unprepare. L'impostazione predefinita per questa opzione può essere modificata chiamando getDefaultServerPreparedStatementDiscardThreshold().|
|void setServerPreparedStatementDiscardThreshold(int value)|Specifica il comportamento per un'istanza di connessione specifica. Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Se l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se è impostata su > 1, queste chiamate vengono raggruppate per evitare un sovraccarico troppo frequente della chiamata di sp_unprepare.|

 **SQLServerDataSource**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Se questa configurazione è impostata su false, la prima esecuzione di un'istruzione preparata chiama sp_executesql e non prepara un'istruzione. La seconda esecuzione chiama sp_prepexec e imposta effettivamente un handle per l'istruzione preparata. Le esecuzioni seguenti chiamano sp_execute. Viene così eliminata la necessità di sp_unprepare alla chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Se questa configurazione restituisce false, la prima esecuzione di un'istruzione preparata chiama sp_executesql e non prepara un'istruzione. La seconda esecuzione chiama sp_prepexec e imposta effettivamente un handle per l'istruzione preparata. Le esecuzioni seguenti chiamano sp_execute. Viene così eliminata la necessità di sp_unprepare alla chiusura dell'istruzione preparata se l'istruzione viene eseguita una sola volta.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Se l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se è impostata su {@literal >} 1, queste chiamate vengono raggruppate per evitare un sovraccarico troppo frequente della chiamata di sp_unprepare|
|int getServerPreparedStatementDiscardThreshold()|Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Se l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se è impostata su {@literal >} 1, queste chiamate vengono raggruppate per evitare un sovraccarico troppo frequente della chiamata di sp_unprepare.|

## <a name="prepared-statement-metatada-caching"></a>Memorizzazione nella cache dei metadati delle istruzioni preparate
A partire dalla versione 6.3.0-anteprima, Microsoft JDBC Driver per SQL Server supporta la memorizzazione nella cache delle istruzioni preparate. Prima della versione 6.3.0-anteprima, se si esegue una query già preparata e archiviata nella cache la chiamata della stessa query non comporta la preparazione. Ora il driver cerca la query nella cache, trova l'handle e lo esegue con sp_execute.
La memorizzazione nella cache dei metadati delle istruzioni preparate è **disabilitata** per impostazione predefinita. Per abilitarla, è necessario chiamare il metodo seguente nell'oggetto connessione:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Ad esempio: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Elenco delle nuove API introdotte con questa modifica, per la memorizzazione nella cache dei metadati delle istruzioni preparate

 **SQLServerConnection**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Imposta il pool di istruzioni su true o false.|
|boolean getDisableStatementPooling()|Restituisce true se il pooling dell'istruzione è disabilitato.|
|void setStatementPoolingCacheSize(int value)|Specifica le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore inferiore a 1 indica nessuna cache.|
|int getStatementPoolingCacheSize()|Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore inferiore a 1 indica nessuna cache.|
|int getStatementHandleCacheEntryCount()|Restituisce il numero corrente di handle di istruzioni preparate in pool.|
|boolean isPreparedStatementCachingEnabled()|Indica se il pooling dell'istruzione è abilitato o meno per questa connessione.|

 **SQLServerDataSource**
 
|Nuovo metodo|Descrizione|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Imposta il pooling dell'istruzione su true o false|
|boolean getDisableStatementPooling()|Restituisce true se il pooling dell'istruzione è disabilitato.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Specifica le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore inferiore a 1 indica nessuna cache.|
|int getStatementPoolingCacheSize()|Restituisce le dimensioni della cache delle istruzioni preparate per questa connessione. Un valore inferiore a 1 indica nessuna cache.|

## <a name="see-also"></a>Vedere anche  
 [Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
