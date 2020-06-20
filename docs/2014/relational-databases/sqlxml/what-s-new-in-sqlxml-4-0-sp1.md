---
title: Novità di SQLXML 4,0 SP1 |&#39;Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
author: rothja
ms.author: jroth
ms.openlocfilehash: 880937520385fbe6ce64be3fdfcbbf7d11c73741
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85009446"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>Novità di SQLXML 4,0 SP1&#39;
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1 sono inclusi diversi aggiornamenti e miglioramenti. In questo argomento viene fornito un riepilogo degli aggiornamenti e vengono riportati i collegamenti a informazioni più dettagliate, se disponibili. In SQLXML 4.0 SP1 sono stati apportati ulteriori miglioramenti per supportare i nuovi tipi di dati introdotti in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Vengono inoltre presentati gli argomenti seguenti:  
  
-   Installazione di SQLXML 4.0 SP1  
  
-   Problemi di installazione affiancata  
  
-   SQLXML 4.0 e MSXML  
  
-   Ridistribuzione di SQLXML 4.0  
  
-   Supporto per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Supporto per i tipi di dati introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
-   Modifiche al caricamento bulk XML per SQLXML 4.0  
  
-   Modifiche alle chiavi del Registro di sistema per SQLXML 4.0  
  
-   Problemi di migrazione  
  
## <a name="installing-sqlxml-40-sp1"></a>Installazione di SQLXML 4.0 SP1  
 Prima di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 veniva rilasciato con SQL Server e apparteneva all'installazione predefinita di tutte le versioni di SQL Server, ad eccezione di SQL Server Express. A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la versione più recente di SQLXML (SQLXML 4.0 SP1) non è più inclusa in SQL Server. Per installare SQLXML 4,0 SP1, scaricarlo dal [percorso di installazione per sqlxml 4,0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 I file di SQLXML 4.0 SP1 vengono installati nel percorso seguente:  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  Tutte le impostazioni del Registro di sistema appropriate per SQLXML 4.0 vengono definite durante il processo di installazione.  
  
 Per consentire l'esecuzione delle applicazioni SQLXML a 32 bit in sistemi operativi WOW64 (Windows on Windows) a 64 bit, eseguire il pacchetto SQLXML 4.0 SP1 a 64 bit, denominato sqlxml4.msi, disponibile nell'Area download Microsoft.  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>Disinstallazione di SQLXML 4.0 SP1  
 In SQLXML 3.0 SP3, SQLXML 4.0 e SQLXML 4.0 SP1 sono presenti chiavi del Registro di sistema condivise. Se le versioni più recenti di SQLXML vengono disinstallate dallo stesso computer su cui è presente SQLXML 3.0 SP3, potrebbe essere necessario reinstallare quest'ultimo.  
  
## <a name="side-by-side-installation-issues"></a>Problemi di installazione affiancata  
 Il processo di installazione di SQLXML 4.0 non determina la rimozione dei file installati da versioni precedenti di SQLXML. È pertanto possibile che in un computer siano presenti le DLL relative a installazioni di diverse versioni di SQLXML. È possibile eseguire installazioni side-by-side. In SQLXML 4.0 sono inclusi sia i PROGID dipendenti sia quelli indipendenti dalla versione. Per tutte le applicazioni di produzione è consigliabile usare i PROGID dipendenti dalla versione.  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 e MSXML  
 SQLXML 4.0 non prevede l'installazione di MSXML, ma l'uso di MSXML 6.0, che viene installato insieme a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva.  
  
## <a name="redistributing-sqlxml-40-sp1"></a>Ridistribuzione di SQLXML 4.0 SP1  
 Per distribuire SQLXML 4.0 SP1, usare il pacchetto del programma di installazione ridistribuibile. Un modo per installare più pacchetti in un'installazione che all'utente può sembrare singola consiste nell'usare la tecnologia del chainer e del programma di avvio automatico. Per altre informazioni, vedere Authoring a Custom Bootstrapper Package for Visual Studio 2005 e Aggiunta di prerequisiti personalizzati.  
  
 Se l'applicazione è destinata a una piattaforma diversa da quella su cui è stata sviluppata, è possibile scaricare versioni di sqlncli.msi per x64, Itanium e x86 dall'Area download Microsoft.  
  
 Sono anche disponibili programmi di installazione di ridistribuzione separati per MSXML 6.0 (msxml6.msi). Tali programmi sono disponibili nel CD di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel percorso seguente:  
  
 `%CD%\Setup\`  
  
 Questi file di installazione possono essere usati per installare MSXML 6.0 direttamente dal CD. Possono inoltre essere usati per ridistribuire liberamente MSXML 6.0 con SQLXML 4.0 SP1 con applicazioni personalizzate.  
  
 È inoltre necessario ridistribuire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se viene usato come provider di dati con l'applicazione. Per altre informazioni, vedere [Installazione di SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="support-for-sql-server-native-client"></a>Supporto per SQL Server Native Client  
 SQLXML 4,0 supporta i provider SQLOLEDB e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. È consigliabile utilizzare la stessa versione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider native client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client è stato sviluppato per supportare i nuovi tipi di dati disponibili nel server, ad esempio i `Date, Time` tipi di `DateTime2` dati, e `dateTimeOffset` in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e supportati da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è una tecnologia di accesso ai dati introdotta in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Questa tecnologia integra il provider SQLOLEDB e il driver SQLODBC in un'unica libreria a collegamento dinamico (DLL) nativa, offrendo contemporaneamente nuove funzionalità diverse da Microsoft Data Access Components (MDAC).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client può essere usato per creare nuove applicazioni o migliorare quelle esistenti che richiedono l'utilizzo delle funzionalità introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non supportate da SQLOLEDB e SQLODBC in MDAC e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è ad esempio necessario per consentire a funzionalità SQLXML sul lato client, come FOR XML, di usare il tipo di dati `xml`. Per ulteriori informazioni, vedere la pagina relativa alla [formattazione XML sul lato Client &#40;SQLXML 4,0&#41;](formatting/client-side-xml-formatting-sqlxml-4-0.md), [utilizzo di ADO per eseguire query SQLXML 4,0](using-ado-to-execute-sqlxml-4-0-queries.md)e [SQL Server Native Client programmazione](../native-client/sql-server-native-client-programming.md).  
  
> [!NOTE]  
>  SQLXML 4.0 non è completamente compatibile con la versione precedente SQLXML 3.0. A causa di alcune correzioni di bug e di altre modifiche funzionali, in modo specifico la rimozione del supporto ISAPI SQLXML, non è possibile usare le directory virtuali IIS con SQLXML 4.0. Anche se la maggior parte delle applicazioni viene eseguita con modifiche minori, è necessario testare le applicazioni prima di metterle in produzione con SQLXML 4.0.  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>Supporto per i tipi di dati introdotti in SQL Server 2005 e SQL Server 2008  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]è stato introdotto il `xml` tipo di dati e SQLXML 4,0 supporta il `xml` tipo di dati. Per ulteriori informazioni, vedere [supporto del tipo di dati XML in SQLXML 4,0](xml-data-type-support-in-sqlxml-4-0.md).  
  
 Per esempi relativi all'utilizzo del tipo di dati `xml` in SQLXML in caso di mapping di viste XML, di caricamento bulk XML o di esecuzione di updategram XML, fare riferimento agli esempi forniti negli argomenti seguenti.  
  
-   [Mapping predefinito di attributi ed elementi XSD a tabelle e colonne](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [Inserimento di dati mediante updategram XML](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [Esempi di caricamento bulk di documenti XML](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]sono stati introdotti i `Date, Time` `DateTime2` tipi di dati, e **DateTimeOffset** . I quattro nuovi tipi di dati vengono abilitati come tipi scalari predefiniti quando SQLXML 4.0 SP1 viene usato con il provider OLE DB di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client (SQLNCLI11), fornito con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>Modifiche al caricamento bulk XML per SQLXML 4.0 SP1  
  
-   Per SQLXML 4,0, il campo di overflow SchemaGen viene creato usando il `xml` tipo di dati. Per ulteriori informazioni, vedere [SQL Server modello a oggetti per il caricamento bulk XML](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md).  
  
-   Se sono state precedentemente create applicazioni [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic e si desidera usare SQLXML 4.0, è necessario ricompilarle con il riferimento a Xblkld4.dll.  
  
-   Per le applicazioni Visual Basic, Scripting Edition è necessario registrare la DLL da usare. Nell'esempio seguente, se si specificano PROGID indipendenti dalla versione, l'applicazione dipende dall'ultima DLL registrata:  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  Il PROGID dipendente dalla versione è SQLXMLBulkLoad.SQLXMLBulkLoad.4.0.  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>Modifiche alle chiavi del Registro di sistema per SQLXML 4.0  
 In SQLXML 4.0 le chiavi del Registro di sistema sono state sostituite rispetto alle versioni precedenti dalle chiavi seguenti.  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 Se si desidera rendere effettive tali chiavi per SQLXML 4.0, è necessario modificare le impostazioni.  
  
 Con SQLXML 4.0 vengono inoltre introdotte le chiavi del Registro di sistema seguenti:  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     Per impostazione predefinita, SQLXML 4.0 restituisce informazioni sugli errori nativi fornite da OLE DB e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], anziché un errore SQLXML di livello elevato (come nel caso delle versioni precedenti di SQLXML). Per evitare questo comportamento, il valore di questa chiave del Registro di sistema di tipo DWORD deve essere impostato su 0 (l'impostazione predefinita è 1).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     Per impostazione predefinita, SQLXML restituisce i valori GUID di SQL Server senza racchiuderli fra parentesi graffe. Se si desidera che il valore GUID venga restituito con le parentesi graffe, ad esempio {*some GUID*}, il valore di questa chiave del registro di sistema deve essere impostato su 1 (l'impostazione predefinita è 0).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     Per impostazione predefinita, quando il parser XML carica i dati, gli spazi vuoti vengono normalizzati in base alle regole di XML 1.0. In questo modo vengono persi alcuni degli spazi vuoti nei dati. La rappresentazione testuale dei dati potrebbe pertanto non essere uguale dopo l'analisi, anche se i dati rimarranno invariati dal punto di vista semantico.  
  
     Questa chiave viene introdotta in modo che sia possibile scegliere di mantenere gli spazi vuoti nei dati. Se si aggiunge tale chiave del Registro di sistema e se ne imposta il valore su 0, gli spazi vuoti (LF, CR e TAB) nei dati XML vengono restituiti codificati nel caso di valori di attributi. Nel caso di valori di elementi, solo il carattere CR viene restituito codificato.  
  
     Ad esempio:  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>Problemi di migrazione  
 Di seguito vengono riportati i problemi che potrebbero avere un impatto sulla migrazione delle applicazioni SQLXML legacy a SQLXML 4.0.  
  
### <a name="ado-and-sqlxml-40-queries"></a>Query ADO e SQLXML 4.0  
 Nelle versioni precedenti di SQLXML viene fornito il supporto per l'esecuzione di query basate sull'URL mediante le directory virtuali IIS e il filtro ISAPI SQLXML. Per le applicazioni che usano SQLXML 4.0 questo supporto non è più disponibile.  
  
 Gli updategram, i modelli e le query SQLXML possono invece essere eseguiti usando le estensioni SQLXML di ActiveX Data Objects (ADO), introdotte per la prima volta con Microsoft Data Access Components (MDAC) 2.6 e versioni successive.  
  
 Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>Supporto per ISAPI SQLXML 3.0 e per i tipi di dati introdotti in SQL Server 2005  
 Poiché il supporto ISAPI è stato rimosso da SQLXML 4,0, se la soluzione richiede le funzionalità avanzate di tipizzazione dei dati introdotte in, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ad esempio il [tipo di dati XML](/sql/t-sql/xml/xml-transact-sql) o i [tipi di dati definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) e l'accesso basato sul Web, sarà necessario utilizzare un'altra soluzione, ad esempio [classi gestite SQLXML](../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md) o un altro tipo di gestore HTTP, ad esempio i servizi Web XML nativi per SQL Server 2005.  
  
 In alternativa, se queste estensioni di tipo non sono necessarie, è possibile continuare a utilizzare SQLXML 3,0 per connettersi alle [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] installazioni di e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] . Il supporto ISAPI SQLXML 3.0 funziona con le versioni più recenti, ma non supporta o riconosce il tipo di dati `xml` o i tipi definiti dall'utente introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>Modifiche alla sicurezza del caricamento bulk XML per i file temporanei  
 Per SQLXML 4.0 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le autorizzazioni per i file del caricamento bulk XML vengono concesse all'utente che esegue l'operazione di caricamento bulk. Le autorizzazioni di lettura e scrittura vengono ereditate dal file system. Nelle versioni precedenti di SQLXML e SQL Server, il caricamento bulk XML in SQLXML crea file temporanei non protetti che potrebbero essere letti da chiunque.  
  
### <a name="migration-issues-for-client-side-for-xml"></a>Problemi di migrazione per FOR XML sul lato client  
 A causa delle modifiche apportate al motore di esecuzione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire valori diversi nei metadati per una tabella di base rispetto a quelli restituiti se la query for XML è stata eseguita con [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] . In questi casi, la formattazione sul lato client dei risultati della query FOR XML presenterà un output differente, a seconda della versione sulla quale viene eseguita la query.  
  
 Se una query FOR XML viene eseguita sul lato client usando SQLXML 3.0 su una colonna con tipo di dati `xml`, i dati dei risultati verranno restituiti sotto forma di stringa sostituita completamente da entità. In SQLXML 4.0, se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) viene specificato come provider, i dati verranno restituiti come XML.  
  
  
