---
title: Linee guida per la programmazione (driver ODBC per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/12/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-makouz
ms.author: genemi
ms.openlocfilehash: bf0961b8ef53060904ad797832e7c7467a859c2b
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79285865"
---
# <a name="programming-guidelines"></a>Linee guida per la programmazione

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Le funzionalità di programmazione di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in macOS e Linux si basano su ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client si basa su ODBC in Windows Data Access Components ([ODBC Programmer's Reference](https://go.microsoft.com/fwlink/?LinkID=45250), Riferimento per i programmatori di ODBC).  

Un'applicazione ODBC può usare MARS (Multiple Active Result Set) e altre funzionalità specifiche di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] includendo `/usr/local/include/msodbcsql.h` dopo le intestazioni unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h` e `sqlucode.h`). Per elementi specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quindi, usare gli stessi nomi simbolici che si userebbero nelle applicazioni ODBC Windows.

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

Il corretto funzionamento delle caratteristiche seguenti non è stato verificato in questa versione del driver ODBC in macOS e Linux:

-   Connessione al cluster di failover
-   [Risoluzione dell'IP di rete trasparente](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (prima di ODBC Driver 17)
-   [Traccia del driver avanzata](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

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
-   SQLBrowseConnect (prima della versione 17.2)
-   I tipi di intervallo C, ad esempio SQL_C_INTERVAL_YEAR_TO_MONTH (documentati nell'articolo relativo a [identificatori e descrittori del tipo di dati](https://msdn.microsoft.com/library/ms716351(VS.85).aspx)) non sono attualmente supportati
-   Valore SQL_CUR_USE_ODBC dell'attributo SQL_ATTR_ODBC_CURSORS della funzione SQLSetConnectAttr.

## <a name="character-set-support"></a>Supporto del set di caratteri

Per ODBC Driver 13 e 13.1 i dati SQLCHAR devono essere in formato UTF-8. Non sono supportate altre codifiche.

Per ODBC Driver 17 sono supportati i dati SQLCHAR in uno dei seguenti set/codifiche di caratteri:

> [!NOTE]  
> A causa delle differenze di `iconv` in `musl` e `glibc`, molte di queste impostazioni locali non sono supportate in Alpine Linux.
>
> Per altre informazioni, vedere [Functional differences from glibc](https://wiki.musl-libc.org/functional-differences-from-glibc.html) (Differenze funzionali da glibc)

|Nome|Descrizione|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latino US|
|CP850|MS-DOS Latino 1|
|CP874|Latino/Thai|
|CP932|Giapponese (Shift-JIS)|
|CP936|Cinese semplificato (GBK)|
|CP949|Coreano EUC-KR|
|CP950|Cinese tradizionale (Big5)|
|CP1251|Cirillico|
|CP1253|Greco|
|CP1256|Arabo|
|CP1257|Baltico|
|CP1258|Vietnamita|
|ISO-8859-1/CP1252|Latino-1|
|ISO-8859-2/CP1250|Latino-2|
|ISO-8859-3|Latino-3|
|ISO-8859-4|Latino-4|
|ISO-8859-5|Latino/Cirillico|
|ISO-8859-6|Latino/Arabo|
|ISO-8859-7|Latino/Greco|
|ISO-8859-8/CP1255|Ebraico|
|ISO-8859-9/CP1254|Turco|
|ISO-8859-13|Latino-7|
|ISO-8859-15|Latino-9|

Al momento della connessione il driver rileva le impostazioni locali correnti del processo nel quale viene caricato. Se il processo usa una delle codifiche precedenti, il driver usa quella codifica per i dati SQLCHAR (caratteri narrow); in caso contrario assume come impostazione predefinita UTF-8. Dato che tutti i processi iniziano con le impostazioni locali "C" per impostazione predefinita (e di conseguenza il driver assume come impostazione predefinita UTF-8), se un'applicazione deve usare una delle codifiche sopra elencate, dovrà usare la funzione **setlocale** per definire correttamente le impostazioni locali, sia specificando in modo esplicito le impostazioni desiderate, sia usando una stringa vuota come `setlocale(LC_ALL, "")` per richiedere l'uso delle impostazioni locali dell'ambiente.

Pertanto in un tipico ambiente Linux o Mac in cui la codifica è UTF-8, gli utenti di ODBC Driver 17 che aggiornano dalla versione 13 o 13.1 non noteranno nessuna differenza. Tuttavia le applicazioni che usano una codifica non UTF-8 inclusa nell'elenco precedente tramite `setlocale()` dovranno usare tale codifica per i dati da e verso il driver, anziché usare UTF-8.

I dati SQLWCHAR devono essere in formato UTF-16LE (Little Endian).

Se quando si esegue il binding di parametri di input con SQLBindParameter è specificato un tipo di carattere SQL narrow come SQL_VARCHAR, il driver converte i dati trasmessi dalla codifica dell'utente alla codifica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] predefinita (in genere la tabella codici 1252). Per i parametri di output il driver esegue la conversione dalla codifica specificata nelle informazioni delle regole di confronto associate ai dati alla codifica del client. Può tuttavia verificarsi la perdita di dati: i caratteri nella codifica di origine non rappresentabili nella codifica di destinazione verranno convertiti in punti interrogativi (?).

Per evitare questo tipo di perdita di dati nel binding dei parametri di input, specificare un tipo di carattere SQL Unicode, ad esempio SQL_NVARCHAR. In questo caso il driver esegue la conversione dalla codifica del client a UTF-16, che può rappresentare tutti i caratteri Unicode. Anche la colonna o il parametro di destinazione nel server deve essere di tipo Unicode (**nchar**, **nvarchar**, **ntext**) o avere regole di confronto/codifica che possono rappresentare tutti i caratteri dei dati di origine. Per evitare la perdita di dati con i parametri di output specificare un tipo Unicode SQL e un tipo Unicode C (SQL_C_WCHAR) (per far sì che il driver restituisca i dati in formato UTF-16) o un tipo C narrow e verificare che la codifica client sia in grado di rappresentare tutti i caratteri dei dati di origine (questo è sempre possibile con UTF-8).

Per altre informazioni sulle regole di confronto e sulle codifiche, vedere [Regole di confronto e supporto Unicode](../../../relational-databases/collations/collation-and-unicode-support.md).

Esistono alcune differenze di conversione della codifica tra Windows e varie versioni della libreria iconv in Linux e macOS. Nei dati di testo codificati nella tabella codici 1255 (Ebraico) un punto di codice (0xCA) si comporta in modo diverso in caso di conversione a Unicode. In Windows questo carattere viene convertito nel punto di codice UTF-16 0x05BA. In macOS e Linux con versioni di libiconv precedenti alla 1.15 viene convertito in 0x00CA. In Linux con le librerie iconv che non supportano la revisione 2003 di Big5/CP950 (denominata `BIG5-2003`) i caratteri aggiunti con questa revisione non vengono convertiti correttamente. Anche nella tabella codici 932 (Giapponese, Shift-JIS) il risultato della decodifica dei caratteri non definiti in origine nello standard di codifica è diverso. Ad esempio il byte 0x80 viene convertito in U+0080 in Windows ma può diventare U+30FB in Linux e macOS, a seconda della versione di iconv.

In ODBC Driver 13 e 13.1, quando caratteri multibyte UTF-8 o caratteri sostitutivi UTF-16 vengono suddivisi tra buffer SQLPutData, i dati vengono danneggiati. Usare i buffer per i flussi SQLPutData che non terminano con la codifica parziale di caratteri. Questa restrizione è stata eliminata con ODBC Driver 17.

## <a name="bkmk-openssl"></a>OpenSSL
A partire dalla versione 17.4, il driver carica OpenSSL in modo dinamico, consentendone l'esecuzione all'interno di sistemi dotati della versione 1.0 o 1.1 senza che siano necessari file di driver distinti. Quando sono presenti più versioni di OpenSSL, il driver tenta di caricare quello più recente. Il driver supporta attualmente OpenSSL 1.0.x e 1.1.x

> [!NOTE]  
> Può verificarsi un conflitto se l'applicazione che usa il driver (o uno dei suoi componenti) è collegata a una versione diversa di OpenSSL o la carica in modo dinamico. Se nel sistema sono presenti diverse versioni di OpenSSL e l'applicazione usa OpenSSL, è consigliabile prestare particolare attenzione affinché la versione caricata dall'applicazione e il driver corrispondano. In caso contrario, infatti, gli errori possono danneggiare la memoria e non presentarsi necessariamente in modo ovvio o coerente.

## <a name="bkmk-alpine"></a>Alpine Linux
Al momento della stesura di questo articolo, la dimensione predefinita dello stack in MUSL è 128 KB, sufficiente per le funzionalità di base del driver ODBC. A seconda delle operazioni svolte dall'applicazione, tuttavia, non è difficile superare questo limite, soprattutto quando si chiama il driver da più thread. È consigliabile compilare un'applicazione ODBC in Alpine Linux con `-Wl,-z,stack-size=<VALUE IN BYTES>` per aumentare la dimensione dello stack. Per riferimento, la dimensione predefinita dello stack nella maggior parte dei sistemi GLIBC è di 2 MB.

## <a name="additional-notes"></a>Note aggiuntive  

1.  È possibile effettuare una connessione amministrativa dedicata (DAC) usando l'autenticazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e **host, porta**. Un membro del ruolo Sysadmin deve prima individuare la porta DAC. Per altre informazioni, vedere [Connessione di diagnostica per gli amministratori di database](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port). Ad esempio, se la porta DAC è 33000, è possibile connettersi a questa porta con `sqlcmd` come indicato di seguito:  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > Le connessioni DAC devono usare l'autenticazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
    
2.  Gestione driver UnixODBC restituisce "Identificatore di opzione o di attributo non valido" per tutti gli attributi di istruzione quando questi vengono passati tramite SQLSetConnectAttr. In Windows, quando SQLSetConnectAttr riceve il valore di un attributo di istruzione, il driver imposta questo valore in tutte le istruzioni attive figlio dell'handle di connessione.  

3.  Quando si usa il driver con applicazioni a elevato multithreading, la convalida degli handle di unixODBC può diventare un collo di bottiglia per le prestazioni. In questi scenari è possibile ottenere prestazioni significativamente maggiori compilando unixODBC con l'opzione `--enable-fastvalidate`. Tenere presente, tuttavia, che a causa di ciò le applicazioni che passano handle non validi alle API ODBC possono subire un arresto anomalo anziché restituire errori `SQL_INVALID_HANDLE`.

## <a name="see-also"></a>Vedere anche  
[Domande frequenti](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Problemi noti in questa versione del driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
