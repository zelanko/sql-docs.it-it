---
title: Utilizzo del buffer adattivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 07a7a67addb10d91b011f821f5b85ed03981d055
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916459"
---
# <a name="using-adaptive-buffering"></a>Utilizzo del buffer adattivo

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La memorizzazione nel buffer adattiva è progettata per recuperare qualsiasi tipo di dati con valori di grandi dimensioni senza l'overhead dei cursori server. Le applicazioni possono usare il buffering adattivo con tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportate dal driver.

In genere, quando [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] esegue una query, il driver recupera tutti i risultati dal server e li carica nella memoria dell'applicazione. Sebbene questo approccio consenta di ridurre al minimo il consumo delle risorse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile che per le query che producono risultati di dimensioni molto grandi venga generato un errore di tipo OutOfMemoryError nell'applicazione JDBC.

Per consentire alle applicazioni di gestire risultati di dimensioni molto grandi, in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è disponibile il buffering adattivo. Grazie al buffering adattivo, il driver può recuperare i risultati dell'esecuzione di istruzioni da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando questi sono necessari per l'applicazione e non tutti contemporaneamente. Quando l'applicazione non necessita più di accedere ai dati, questi vengono inoltre eliminati dal driver. Di seguito sono illustrati alcuni esempi di casi in cui il buffer adattivo può rivelarsi utile:

- **La query produce un set di risultati di dimensioni molto grandi:** L'applicazione può eseguire un'istruzione SELECT che produce più righe di quelle che l'applicazione può archiviare in memoria. Nelle versioni precedenti era necessario che l'applicazione usasse un cursore server per evitare un errore di tipo OutOfMemoryError. Il buffer adattivo consente di passare in modalità forward-only di sola lettura un set di risultati anche molto grande senza che sia necessario un cursore server.

- **La query produce dimensioni molto grandi** [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) **colonne o** [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) **Valori dei parametri out:** L'applicazione può recuperare un singolo valore (colonna o parametro OUT) troppo grande per adattarsi interamente alla memoria dell'applicazione. Il buffer adattivo consente all'applicazione client di recuperare tale valore come flusso, usando i metodi getAsciiStream, getBinaryStream o getCharacterStream. L'applicazione recupera il valore da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] leggendolo dal flusso.

> [!NOTE]  
> Con il buffer adattivo il driver JDBC memorizza nel buffer solo la quantità di dati necessaria e non fornisce alcun metodo pubblico per controllare o limitare le dimensioni del buffer.

## <a name="setting-adaptive-buffering"></a>Impostazione del buffer adattivo

A partire dalla versione 2.0 del driver JDBC, il comportamento predefinito del driver è "**adattivo**". In altre parole, per ottenere il comportamento del buffer adattivo in questa versione, l'applicazione non deve richiederlo in modo esplicito. Nella versione 1.2, tuttavia, la modalità di buffering predefinita è "**completa**" e l'applicazione deve richiedere la modalità di buffering adattivo in modo esplicito.

Un'applicazione può richiedere l'utilizzo del buffer adattivo nell'esecuzione di un'istruzione in tre modi:

- L'applicazione può impostare la proprietà di connessione **responseBuffering** su "Adaptive". Per ulteriori informazioni sull'impostazione delle proprietà di connessione, vedere [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).

- L'applicazione può usare il metodo [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) dell'oggetto [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) per impostare la modalità di memorizzazione delle risposte nel buffer per tutte le connessioni create tramite tale oggetto [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).

- L'applicazione può usare il metodo [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) per impostare la modalità di memorizzazione delle risposte nel buffer per un oggetto istruzione specifico.

Quando si usa la versione 1.2 del driver JDBC, le applicazioni devono eseguire il cast dell'oggetto istruzione in una classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) per applicare il metodo [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md). Gli esempi di codice nell'esempio di [lettura di dati di grandi dimensioni](../../connect/jdbc/reading-large-data-sample.md) e la [lettura di dati di grandi dimensioni con stored procedure](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) illustrano questo utilizzo obsoleto.

Con la versione 2.0 del driver JDBC, tuttavia, le applicazioni possono usare i metodi [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) per accedere a funzionalità specifiche del fornitore senza presupporre l'implementazione della gerarchia di classi. Per un esempio di codice, vedere l'argomento relativo all' [aggiornamento di dati di grandi dimensioni](../../connect/jdbc/updating-large-data-sample.md) .

## <a name="retrieving-large-data-with-adaptive-buffering"></a>Recupero di dati di grandi dimensioni con il buffer adattivo

Quando si usano i metodi get[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Type>Stream per leggere valori di grandi dimensioni una volta e si esegue l'accesso alle colonne ResultSet e ai parametri OUT CallableStatement nell'ordine restituito da \<, il buffer adattivo consente di ridurre al minimo l'utilizzo della memoria dell'applicazione durante l'elaborazione dei risultati. Quando si utilizza il buffer adattivo, si verifica quanto indicato di seguito:

- I metodi get\<Type>Stream definiti nelle classi [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) restituiscono per impostazione predefinita flussi che possono essere letti una sola volta, sebbene possano essere reimpostati, se contrassegnati dall'applicazione. Per applicare il metodo `reset` al flusso, l'applicazione deve prima chiamare il metodo `mark` su tale flusso.

- I metodi get\<Type>Stream definiti nelle classi [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) e [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) restituiscono flussi che possono essere sempre spostati nella posizione iniziale del flusso senza chiamare il metodo `mark`.

Quando l'applicazione usa il buffer adattivo, i valori recuperati dai metodi get\<Type>Stream possono essere recuperati una sola volta. Se si tenta di chiamare qualsiasi metodo get\<Type> method sulla stessa colonna o sullo stesso parametro dopo avere chiamato il metodo get\<Type>Stream dello stesso oggetto, verrà generata un'eccezione con il messaggio "Accesso ai dati eseguito. Dati non disponibili per questa colonna o questo parametro".

> [!NOTE]
> Una chiamata a ResultSet. Close () durante l'elaborazione di un ResultSet richiederebbe a Microsoft JDBC driver per SQL Server di leggere ed eliminare tutti i pacchetti rimanenti. Questa operazione può richiedere molto tempo se la query ha restituito un set di dati di grandi dimensioni e soprattutto se la connessione di rete è lenta.

## <a name="guidelines-for-using-adaptive-buffering"></a>Linee guida per l'utilizzo del buffer adattivo

Per ridurre al minimo l'utilizzo della memoria da parte dell'applicazione, gli sviluppatori devono attenersi alle importanti linee guida seguenti:

- Evitare di usare la proprietà della stringa di connessione **selectMethod=cursor** per consentire all'applicazione di elaborare un set di risultati di dimensioni molto grandi. La caratteristica di buffer adattivo consente alle applicazioni di elaborare set di risultati forward-only di sola lettura di dimensioni molto grandi senza utilizzare un cursore server. Si noti che l'impostazione di **selectMethod=cursor** influisce su tutti i set di risultati forward-only di sola lettura prodotti da tale connessione. In altre parole, se l'applicazione elabora regolarmente set di risultati brevi contenenti poche righe, per la creazione, la lettura e la chiusura di un cursore server per ogni set di risultati sia sul lato server che sul lato client verrà usato un maggior numero di risorse rispetto a quando **selectMethod** non è impostato su **cursor**.

- Leggere i valori binari o di testo di grandi dimensioni come flussi usando i metodi getAsciiStream, getBinaryStream o getCharacterStream anziché i metodi GetBlob o getClob. A partire dalla versione 1.2, nella classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) sono disponibili nuovi metodi get\<Type>Stream da usare a questo scopo.

- Assicurarsi che le colonne con valori potenzialmente grandi siano posizionate per ultime nell'elenco di colonne in un'istruzione SELECT e che i metodi \<Type>Stream di [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) vengano usati per accedere alle colonne nell'ordine in cui vengono selezionate.

- Assicurarsi che i parametri OUT con valori potenzialmente grandi siano dichiarati per ultimi nell'elenco di parametri nel linguaggio SQL usato per creare [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Assicurarsi anche che i metodi get\<Type>Stream di [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) vengano usati per accedere ai parametri OUT nell'ordine in cui vengono dichiarati.

- Evitare di eseguire simultaneamente più di un'istruzione nella stessa connessione. Se viene eseguita un'altra istruzione prima dell'elaborazione dei risultati dell'istruzione precedente, i risultati non elaborati potrebbero venire memorizzati nel buffer della memoria dell'applicazione.

- In alcuni casi, l'utilizzo di **SelectMethod = Cursor** anziché **responseBuffering = adaptive** è più vantaggioso, ad esempio:

  - Se l'applicazione elabora lentamente un set di risultati di sola lettura, come la lettura di ogni riga dopo un input dell'utente, l'utilizzo di **SelectMethod = Cursor** anziché **responseBuffering = adaptive** potrebbe contribuire a ridurre l'utilizzo delle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] risorse da parte di .

  - Se l'applicazione elabora due o più set di risultati forward-only di sola lettura contemporaneamente nella stessa connessione, l'uso di **selectMethod=cursor** anziché **responseBuffering=adaptive** può contribuire a ridurre la memoria richiesta dal driver durante l'elaborazione dei set di risultati.

  In entrambi i casi, è opportuno considerare l'overhead generato dalla creazione, dalla lettura e dalla chiusura dei cursori server.

Nel seguente elenco vengono inoltre fornite alcune indicazioni relative ai set di risultati scorrevoli e forward-only aggiornabili.

- Per i set di risultati scorrevoli, durante il recupero di un blocco di righe, il driver legge sempre in memoria il numero di righe indicate dal metodo [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), anche quando il buffering adattivo è abilitato. Se lo scorrimento genera un errore di tipo OutOfMemoryError, è possibile ridurre il numero di righe recuperate chiamando il metodo [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) per impostare le dimensioni del recupero su un numero minore di righe, anche su una se necessario. Se in tal modo non si previene l'errore di tipo OutOfMemoryError, non includere colonne particolarmente estese nei set di risultati scorrevoli.

- Per i set di risultati forward-only aggiornabili, durante il recupero di un blocco di righe, il driver legge in genere in memoria il numero di righe indicate dal metodo [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), anche quando il buffering adattivo è abilitato per la connessione. Se chiamando il metodo [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) viene restituito un errore di tipo OutOfMemoryError, è possibile ridurre il numero di righe recuperate chiamando il metodo [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) per impostare le dimensioni del recupero su un numero minore di righe, anche su una se necessario. È anche possibile forzare il driver a non memorizzare nel buffer alcuna riga chiamando il metodo [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) dell'oggetto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) con il parametro "**adaptive**" prima di eseguire l'istruzione. Poiché il set di risultati non è scorrevole, se l'applicazione accede a un valore di colonna di grandi dimensioni usando uno dei metodi get\<Type>Stream, il driver eliminerà il valore non appena verrà letto dall'applicazione, come avviene per i set di risultati forward-only di sola lettura.

## <a name="see-also"></a>Vedere anche

[Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
