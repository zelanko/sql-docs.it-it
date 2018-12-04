---
title: Linee guida per programmatori (Driver ODBC per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a8fa77ed1819d22eb90ea4fb0a7308122f708e1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522951"
---
# <a name="programming-guidelines"></a>Linee guida per la programmazione

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Le funzionalità di programmazione di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in macOS e Linux si basano su ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client si basa su ODBC in Windows Data Access Components ([ODBC Programmer's Reference](https://go.microsoft.com/fwlink/?LinkID=45250), Riferimento per i programmatori di ODBC).  

Un'applicazione ODBC può utilizzare Multiple Active Result Set (MARS) e altri [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specifiche funzionalità includendo `/usr/local/include/msodbcsql.h` dopo aver incluso le intestazioni unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h`, e `sqlucode.h`). Per elementi specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quindi, usare gli stessi nomi simbolici che si userebbero nelle applicazioni ODBC Windows.

## <a name="available-features"></a>Funzionalità disponibili  
Quando si usa il driver ODBC in macOS o Linux, sono valide le sezioni seguenti della documentazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client for ODBC ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)):  

-   [Comunicazione con SQL Server (ODBC)](https://msdn.microsoft.com/library/ms131692.aspx)  
-   [Supporto del timeout della connessione e delle query](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [Cursori](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [Miglioramenti relativi a data e ora (ODBC)](https://msdn.microsoft.com/library/bb677319.aspx)  
-   [Esecuzione di query (ODBC)](https://msdn.microsoft.com/library/ms131677.aspx)  
-   [Gestione di errori e messaggi](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Autenticazione Kerberos](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [Tipi CLR definiti dall'utente di grandi dimensioni (ODBC)](https://msdn.microsoft.com/library/bb677316.aspx)  
-   [Esecuzione di transazioni (ODBC) (escluse le transazioni distribuite)](https://msdn.microsoft.com/library/ms131706.aspx)  
-   [Risultati dell'elaborazione (ODBC)](https://msdn.microsoft.com/library/ms130812.aspx)  
-   [Esecuzione delle stored procedure](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [Supporto per colonne di tipo sparse (ODBC)](https://msdn.microsoft.com/library/cc280357.aspx)
-   [Crittografia SSL](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [Parametri con valori di tabella](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 e UTF-16 per l'interfaccia API dei comandi e dei dati](https://msdn.microsoft.com/library/ff878241.aspx)
-   [Uso delle funzioni catalogo](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>Caratteristiche non supportate

Le funzionalità seguenti non sono state verificate funzionava correttamente in questa versione del driver ODBC in macOS e Linux:

-   Connessione al Cluster di failover
-   [Risoluzione dell'IP di rete trasparente](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (prima di ODBC Driver 17)
-   [Traccia Driver avanzate](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Le funzionalità seguenti non sono disponibili in questa versione del driver ODBC in macOS e Linux: 

-   Transazioni distribuite (l'attributo SQL_ATTR_ENLIST_IN_DTC non è supportato)  
-   Mirroring del database  
-   FILESTREAM  
-   Profilatura delle prestazioni del driver ODBC, descritta in [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=234099) e gli attributi di connessione correlati alle prestazioni seguenti:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   I tipi di intervallo C, ad esempio SQL_C_INTERVAL_YEAR_TO_MONTH (documentati nell'articolo relativo a [identificatori e descrittori del tipo di dati](https://msdn.microsoft.com/library/ms716351(VS.85).aspx)) non sono attualmente supportati
-   Valore SQL_CUR_USE_ODBC dell'attributo SQL_ATTR_ODBC_CURSORS della funzione SQLSetConnectAttr.

## <a name="character-set-support"></a>Supporto del set di caratteri

Per ODBC Driver 13 e 13.1, i dati SQLCHAR devono essere UTF-8. Altre codifiche non sono supportati.

Per ODBC Driver 17, i dati SQLCHAR in uno dei seguenti gruppi/codifiche di caratteri sono supportati:

|nome|Descrizione|
|-|-|
|UTF-8|Unicode|
|CP437|Alfabeto latino MS-DOS degli Stati Uniti|
|CP850|Latino 1 MS-DOS|
|CP874|Alfabeto latino/Thai|
|CP932|Giapponese (Shift-JIS)|
|CP936|Cinese semplificato (GBK)|
|CP949|Coreano EUC-KR|
|CP950|Cinese tradizionale (Big5)|
|CP1251|Cirillico|
|CP1253|Greco|
|CP1256|Arabo|
|CP1257|Baltico|
|CP1258|Vietnamita|
|ISO-8859-1 / CP1252|Latino 1|
|ISO-8859-2 / CP1250|Latino 2|
|ISO-8859-3|Latino 3|
|ISO-8859-4|Alfabeto latino-4|
|ISO 8859-5|Alfabeto latino/cirillico|
|ISO-8859-6|Alfabeto latino/arabo|
|ISO-8859-7|Alfabeto latino/greco|
|ISO-8859-8 / CP1255|Ebraico|
|ISO-8859-9 / CP1254|Turco|
|ISO-8859-13|Alfabeto latino a 7|
|ISO 8859-15|Latino 9|

Al momento della connessione, il driver rileva le impostazioni locali correnti del processo che viene caricato. Se Usa una delle codifiche descritte sopra, il driver usa tale codifica per i dati SQLCHAR (caratteri "narrow"); in caso contrario, l'impostazione predefinita è UTF-8. Poiché tutti i processi avviati per impostazione predefinita nelle impostazioni locali "C" (e pertanto causare il driver per impostazione predefinita in UTF-8), se un'applicazione deve usare una delle codifiche descritte sopra, è necessario usare il **setlocale** configurare le impostazioni locali in modo appropriato prima (funzione) la connessione; specificare le impostazioni locali desiderate in modo esplicito, o utilizzando una stringa vuota, ad esempio `setlocale(LC_ALL, "")` usare le impostazioni locali dell'ambiente.

Di conseguenza, in un Mac o Linux ambiente tipico in cui la codifica è UTF-8, gli utenti di ODBC Driver 17 l'aggiornamento da 13 o 13.1 non rispetterà eventuali differenze. Tuttavia, le applicazioni che usano una codifica non UTF-8 nell'elenco precedente tramite `setlocale()` necessario usare tale codifica per i dati da e verso il driver anziché UTF-8.

I dati SQLWCHAR devono essere in formato UTF-16LE (Little Endian).

Quando si associano parametri di input con SQLBindParameter, se un carattere narrow SQL digitare, ad esempio SQL_VARCHAR viene specificato, il driver converte i dati forniti dal client di codifica per il valore predefinito (in genere la tabella codici 1252) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] codifica. Per i parametri di output, il driver converte dalla codifica specificata nelle informazioni di regole di confronto associate ai dati al client di codifica. Tuttavia, potrebbe verificarsi una perdita dei dati---caratteri nella codifica di origine non rappresentabile nella codifica di destinazione verranno convertito in un punto interrogativo ('? ').

Per evitare la perdita di dati quando si associano parametri di input, specificare un tipo di carattere SQL Unicode, ad esempio SQL_NVARCHAR. In questo caso, il driver converte dal client di codifica UTF-16, che possono rappresentare tutti i caratteri Unicode. Inoltre, la colonna di destinazione o il parametro nel server deve inoltre essere un tipo di Unicode (**nchar**, **nvarchar**, **ntext**) o a uno con delle regole di confronto/codifica, che può essere rappresenta tutti i caratteri di dati di origine. Per evitare la perdita di dati con i parametri di output, specificare un tipo SQL Unicode e un Unicode C tipo (SQL_C_WCHAR), causando il driver restituire dati come UTF-16; o C narrow digitare e verificare che il client di codifica può rappresentare tutti i caratteri dei dati di origine (questo è sempre possibile eseguire con UTF-8).

Per altre informazioni sulle regole di confronto e sulle codifiche, vedere [Regole di confronto e supporto Unicode](../../../relational-databases/collations/collation-and-unicode-support.md).

Esistono alcune differenze di conversione di codifica tra versioni diverse della libreria iconv in Linux e macOS e Windows. I dati di testo nella tabella codici 1255 (ebraico) dispone di un punto di codice (0xCA) che si comporta in modo diverso durante la conversione in Unicode. In Windows, questo carattere converte il punto di codice UTF-16 pari a 0x05BA. In macOS e Linux con libiconv precedenti alla versione 1.15, converte in a 0x00CA. In Linux con le librerie iconv che non supportano la revisione 2003 di Big5/CP950 (denominato `BIG5-2003`), caratteri aggiunti con tale revisione non convertirà correttamente. Nella tabella codici 932 (Japanese, Shift-JIS), il risultato di decodifica di caratteri non originariamente definiti nello standard di codifica è diversa anche. Ad esempio, il byte 0x80 converte da u+0080 su Windows ma può diventare 30FB U + in Linux e macOS, a seconda della versione iconv.

In ODBC Driver 13 e 13.1, quando caratteri multibyte UTF-8 o caratteri sostitutivi UTF-16 vengono suddivisi tra buffer SQLPutData, i dati vengono danneggiati. Usare i buffer per i flussi SQLPutData che non terminano con la codifica parziale di caratteri. Questa limitazione è stata rimossa con ODBC Driver 17.

## <a name="additional-notes"></a>Note aggiuntive  

1.  È possibile effettuare una connessione amministrativa dedicata (DAC) usando l'autenticazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e **host, porta**. Un membro del ruolo Sysadmin deve prima individuare la porta DAC. Visualizzare [connessione di diagnostica per gli amministratori di Database](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) per individuare la modalità. Ad esempio, se la porta DAC è 33000, è possibile connettersi a questa porta con `sqlcmd` come indicato di seguito:  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > Le connessioni DAC devono usare l'autenticazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
    
2.  Gestione driver UnixODBC restituisce "Identificatore di opzione o di attributo non valido" per tutti gli attributi di istruzione quando questi vengono passati tramite SQLSetConnectAttr. In Windows, quando SQLSetConnectAttr riceve il valore di un attributo di istruzione, il driver imposta questo valore in tutte le istruzioni attive figlio dell'handle di connessione.  

## <a name="see-also"></a>Vedere anche  
[Domande frequenti](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Problemi noti in questa versione del driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes.md)
