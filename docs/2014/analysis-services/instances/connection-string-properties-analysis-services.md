---
title: Proprietà della stringa di connessione (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 29a00a41-5b0d-44b2-8a86-1b16fe507768
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83ead8522e506fcf4ab81d2e904c354424cdb6fd
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080163"
---
# <a name="connection-string-properties-analysis-services"></a>Proprietà delle stringhe di connessione (Analysis Services)
  In questo argomento vengono illustrate le proprietà delle stringhe di connessione che è possibile impostare in uno degli strumenti di progettazione o di amministrazione o trovare nelle stringhe di connessione create dalle applicazioni client che si connettono ai dati di Analysis Services ed eseguono query su di essi. Viene pertanto preso in considerazione solo un subset delle proprietà disponibili. L'elenco completo include numerose proprietà del server e del database attraverso cui è possibile personalizzare una connessione per un'applicazione specifica indipendentemente dal tipo di configurazione dell'istanza o del database nel server.  
  
 È consigliabile che gli sviluppatori responsabili della compilazione di stringhe di connessione nel codice delle applicazioni consultino la documentazione dell'API per client ADOMD.NET in cui è disponibile un elenco più dettagliato: <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 Le proprietà descritte in questo argomento vengono usate dalle librerie client di Analysis Services, da ADOMD.NET, da AMO e dal provider OLE DB per Analysis Services. La maggior parte delle proprietà delle stringhe di connessione è utilizzabile con tutte e tre le librerie client. Le eccezioni sono indicate nella descrizione.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Parametri di connessione di uso comune](#bkmk_common)  
  
 [Autenticazione e sicurezza](#bkmk_auth)  
  
 [Parametri per scopi specifici](#bkmk_special)  
  
 [Riservate per utilizzo futuro](#bkmk_reserved)  
  
 [Esempi di stringhe di connessione](#bkmk_examples)  
  
 [Formati di stringa di connessione usati in Analysis Services](#bkmk_supportedstrings)  
  
 [Crittografia di stringhe di connessione](#bkmk_encrypt)  
  
> [!NOTE]  
>  Se durante la configurazione delle proprietà si imposta inavvertitamente la stessa proprietà due volte, nella stringa di connessione viene usato l'ultimo valore.  
  
 Per altre informazioni su come specificare una connessione ad Analysis Services in applicazioni Microsoft esistenti, vedere [Connessione dalle applicazioni client &#40;Analysis Services&#41;](connect-from-client-applications-analysis-services.md).  
  
##  <a name="bkmk_common"></a> Parametri di connessione di uso comune  
 Nella tabella seguente vengono descritte le proprietà di utilizzo più frequente per la compilazione di una stringa di connessione.  
  
|Proprietà|Descrizione|Esempio|  
|--------------|-----------------|-------------|  
|`Data Source` o `DataSource`|Specifica l'istanza del server. Questa proprietà è obbligatoria per tutte le connessioni. I valori validi includono il nome di rete o l'indirizzo IP del server, local o localhost per le connessioni locali, l'URL se il server è configurato per l'accesso HTTP o HTTPS oppure il nome di un file di cubo locale (con estensione cub).|`Data source=AW-SRV01` per l'istanza e la porta predefinite (TCP 2383).<br /><br /> `Data source=AW-SRV01$Finance:8081` per un'istanza denominata ($Finance) e una porta fissa.<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` per un nome di dominio completo, presupponendo che si utilizzino l'istanza e la porta predefinite.<br /><br /> `Data source=172.16.254.1` per un indirizzo IP del server in modo da ignorare la ricerca nel server DNS, utile per la risoluzione dei problemi di connessione.|  
|`Initial Catalog` o `Catalog`|Specifica il nome del database di Analysis Services a cui connettersi. Il database deve essere distribuito in Analysis Services e l'utente deve disporre delle autorizzazioni necessarie per la connessione. Questa proprietà è facoltativa per le connessioni AMO, ma obbligatoria per ADOMD.NET.|`Initial catalog=AdventureWorks2012`|  
|`Provider`|I valori validi includono MSOLAP o MSOLAP. \<versione >, dove \<versione > è 3, 4 o 5. Nel file system il nome del provider di dati è msolap110.dll per la versione SQL Server 2012, msolap100.dll per SQL Server 2008 e 2008 R2 e msolap90.dll per SQL Server 2005.<br /><br /> La versione corrente è MSOLAP.5. Questa proprietà è facoltativa. Per impostazione predefinita, le librerie client leggono la versione corrente del provider OLE DB dal Registro di sistema. È necessario impostare questa proprietà solo se occorre una versione specifica del provider di dati, ad esempio per la connessione a un'istanza di SQL Server 2008.<br /><br /> I provider di dati corrispondono alle versioni di SQL Server. Se l'organizzazione usano la versione corrente e le versioni precedenti di Analysis Services, sarà probabilmente necessario specificare il provider da usare nelle stringhe di connessione create manualmente. Potrebbe inoltre essere necessario scaricare e installare versioni specifiche del provider di dati in computer che non dispongono della versione richiesta. È possibile scaricare il provider OLE DB dalle pagine del Feature Pack di SQL Server nell'Area download. Visitare la pagina [Feature Pack di Microsoft SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=296473) per scaricare il provider OLE DB di Analysis Services per SQL Server 2012.<br /><br /> MSOLAP.4 è stato rilasciato sia in SQL Server 2008 sia in SQL Server 2008 R2. La versione 2008 R2 supporta le cartelle di lavoro PowerPivot ed è talvolta necessario installarlo manualmente nei server SharePoint. Per distinguere tra queste versioni, è necessario controllare il numero di build nelle proprietà del file del provider: Passare a Programmi\Microsoft Analysis Services\AS OLEDB\10. Fare clic con il pulsante destro del mouse sul file msolap110.dll e scegliere **Proprietà**. Scegliere **Dettagli**. Visualizzare le informazioni sulla versione del file. La versione deve includere 10.50. \<NumeroBuild > per SQL Server 2008 R2. Per altre informazioni, vedere [Installare il provider OLE DB di Analysis Services nei server di SharePointt](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) e [Provider di dati usati per le connessioni ad Analysis Services](data-providers-used-for-analysis-services-connections.md).<br /><br /> MSOLAP.3 rilasciato in SQL Server 2005.<br /><br /> MSOLAP.4 è stato rilasciato in SQL Server 2008 e nuovamente in SQL Server 2008 R2<br /><br /> MSOLAP.5 rilasciato in SQL Server 2012|`Provider=MSOLAP.3` viene usato per le connessioni che richiedono la versione di SQL Server 2005 del provider OLE DB per Analysis Services.|  
|`Cube`|Nome del cubo o della prospettiva. Un database può contenere più cubi e prospettive. Se sono possibili più destinazioni, includere il nome del cubo o della prospettiva nella stringa di connessione.|`Cube=SalesPerspective` indica che è possibile usare la proprietà Cube della stringa di connessione per specificare il nome di un cubo o di una prospettiva.|  
  
##  <a name="bkmk_auth"></a> Autenticazione e sicurezza  
 In questa sezione sono illustrate le proprietà delle stringhe di connessione correlate all'autenticazione e alla crittografia. Per Analysis Services si usano solo l'autenticazione di Windows ma è possibile impostare nella stringa di connessione proprietà che consentono di passare una combinazione specifica di nome utente e password.  
  
 Le proprietà sono elencate in ordine alfabetico.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`EffectiveUserName`|Usare questa proprietà quando nel server deve essere rappresentata l'identità di un utente finale. Specificare l'account nel formato dominio\utente. Per usare questa proprietà, il chiamante deve disporre di autorizzazioni amministrative in Analysis Services. Per altre informazioni sull'utilizzo di questa proprietà in una cartella di lavoro di Excel da SharePoint, vedere [Usare EffectiveUserName di Analysis Services in SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkId=311905). Per una spiegazione della modalità di utilizzo di questa proprietà con Reporting Services, vedere la pagina relativa all' [utilizzo di EffectiveUserName per la rappresentazione in SSAS](https://www.artisconsulting.com/blogs/greggalloway/2010/4/1/using-effectiveusername-to-impersonate-in-ssas).<br /><br /> La proprietà `EffectiveUserName` viene usata in un'installazione di PowerPivot per SharePoint allo scopo di acquisire informazioni sull'utilizzo. L'identità dell'utente viene fornita al server in modo che sia possibile registrare nei file di log eventi ed errori che includono tale identità. Nel caso di PowerPivot, non viene usata a fini di autorizzazione.|  
|**Encrypt Password**|Specifica se deve essere usata una password locale per crittografare cubi locali. I valori validi sono True o False. Il valore predefinito è False.|  
|`Encryption Password`|Password usata per decrittografare un cubo locale crittografato. Il valore predefinito è vuoto. Questo valore deve essere impostato dall'utente in modo esplicito.|  
|`Impersonation Level`|Indica il livello di rappresentazione che il server è autorizzato a usare per rappresentare il client. I valori validi includono:<br /><br /> **Anonimo**: Il client è anonimo per il server. Il processo server non può ottenere informazioni sul client né quest'ultimo può essere rappresentato.<br /><br /> **Identificare**: Il processo server può ottenere l'identità del client. Il server può rappresentare l'identità del client a fini di autorizzazione ma non può accedere a oggetti di sistema con tale identità.<br /><br /> **Rappresentare**: Rappresenta il valore predefinito. L'identità del client può essere rappresentata, ma solo quando viene stabilita la connessione e non a ogni chiamata.<br /><br /> **Delegato**: Il processo server può rappresentare il contesto di sicurezza del client quando agisce per conto del client. Il processo server può inoltre effettuare chiamate in uscita ad altri server quando agisce per conto del client.|  
|`Integrated Security`|Per la connessione ad Analysis Services viene usata l'identità di Windows del chiamante. I valori validi sono vuoto, SSPI e BASIC.<br /><br /> `Integrated Security`=`SSPI` è il valore predefinito per le connessioni TCP, consente l'autenticazione anonima, NTLM o Kerberos. Il valore vuoto è quello predefinito per le connessioni HTTP.<br /><br /> Quando si utilizza `SSPI`, è necessario impostare `ProtectionLevel` su uno dei valori seguenti: `Connect`, `PktIntegrity`, `PktPrivacy`.|  
|`Persist Encrypted`|Impostare questa proprietà se l'applicazione client richiede l'oggetto origine dati per rendere persistenti le informazioni di autenticazione riservate, ad esempio una password, in formato crittografato. Per impostazione predefinita, le informazioni non sono persistenti.|  
|`Persist Security Info`|I valori validi sono True e False. Se impostata su True, le informazioni di sicurezza quali l'identità dell'utente o la password precedentemente specificate nella stringa di connessione possono essere ottenute dalla connessione dopo che quest'ultima è stata stabilita. Il valore predefinito è False.|  
|`ProtectionLevel`|Determina il livello di sicurezza usato per la connessione. I valori validi sono:<br /><br /> `None` (Indici per tabelle con ottimizzazione per la memoria). Connessioni non autenticate o anonime. Non viene eseguita alcuna autenticazione per i dati inviati al server.<br /><br /> `Connect` (Indici per tabelle con ottimizzazione per la memoria). Connessioni autenticate. L'autenticazione viene eseguita solo quando il client stabilisce una relazione con un server.<br /><br /> `PktIntegrity` (Indici per tabelle con ottimizzazione per la memoria). Connessioni crittografate Viene verificato che tutti i dati inviati dal client siano stati ricevuti e che durante il transito non siano state apportate modifiche.<br /><br /> `PktPrivacy` (Indici per tabelle con ottimizzazione per la memoria). Crittografia con firma, supportata solo per XMLA. Viene verificato che tutti i dati inviati dal client siano stati ricevuti senza modifiche apportate durante il transito e viene assicurata la protezione della privacy dei dati mediante crittografia.<br /><br /> <br /><br /> Per altre informazioni, vedere [Establishing Secure Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections)|  
|`Roles`|Specificare un elenco con valori delimitati da virgole dei ruoli predefiniti per la connessione a un server o a un database mediante le autorizzazioni trasmesse dal ruolo in questione. Se questa proprietà viene omessa, vengono usati tutti i ruoli e le autorizzazioni valide derivano da una combinazione di tutti i ruoli. Impostando la proprietà su un valore vuoto (ad esempio, Roles =' ') della connessione client non dispone di alcun ruolo.<br /><br /> Un amministratore che usano questa proprietà si connette con le autorizzazioni trasmesse dal ruolo. Alcuni comandi potrebbero avere esito negativo se il ruolo non fornisce autorizzazioni sufficienti.|  
|`SSPI`|Specifica in modo esplicito il pacchetto di sicurezza da usare per l'autenticazione client quando `Integrated Security` è impostato su `SSPI`. SSPI supporta più pacchetti, tuttavia è possibile usare questa proprietà per specificare un pacchetto particolare. I valori validi sono Negotiate, Kerberos, NTLM e Anonymous User. Se questa proprietà non è impostata, per la connessione saranno disponibili tutti i pacchetti.|  
|`Use Encryption for Data`|Crittografa le trasmissioni di dati. I valori validi sono True e False.|  
|`User ID`=...; `Password`=|`User ID` e `Password` vengono usati insieme. Analysis Services rappresenta l'identità dell'utente specificata tramite queste credenziali. Per le connessioni ad Analysis Services, si ricorre all'inserimento delle credenziali nella riga di comando solo se il server è configurato per l'accesso HTTP e si è specificata l'autenticazione di base invece della sicurezza integrata per la directory virtuale di IIS.<br /><br /> Il nome utente e password devono essere le credenziali di un'identità di Windows, ovvero un account utente locale o di dominio. Si noti che `User ID` presenta uno spazio incorporato. Altri alias per questa proprietà includono `UserName` (senza spazio) e `UID`. L'alias per `Password` è `PWD`.|  
  
##  <a name="bkmk_special"></a> Parametri per scopi specifici  
 In questa sezione vengono descritti i parametri rimanenti delle stringhe di connessione. Questi parametri vengono usati per assicurare specifici comportamenti di connessione richiesti da un'applicazione.  
  
 Le proprietà sono elencate in ordine alfabetico.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`Application Name`|Imposta il nome dell'applicazione associata alla connessione. Questo valore può essere utile per il monitoraggio degli eventi di traccia, in particolar modo se più applicazioni accedono agli stessi database. Ad esempio, si aggiunge Application Name = 'test' a le cause di stringa di connessione 'test' venga visualizzato in una traccia di SQL Server Profiler, come illustrato nello screenshot seguente:<br /><br /> ![SSAS_AppNameExcample](../media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> Gli alias per questa proprietà includono `sspropinitAppName`, `AppName`. Per altre informazioni, vedere la pagina relativa all' [utilizzo del parametro Application Name per la connessione a SQL Server](https://go.microsoft.com/fwlink/?LinkId=301699).|  
|`AutoSyncPeriod`|Imposta la frequenza (in millisecondi) della sincronizzazione della cache di client e server. ADOMD.NET offre la memorizzazione nella cache del client per oggetti di utilizzo frequente con overhead di memoria minimo. Ciò consente di ridurre il numero di round trip al server. L'impostazione predefinita è 10000 millisecondi (o 10 secondi). Se è impostata su null o 0, la sincronizzazione automatica è disabilitata.|  
|`Character Encoding`|Definisce la modalità di codifica dei caratteri nella richiesta. I valori validi sono Default o UTF-8 (equivalenti) e UTF-16|  
|`CompareCaseSensitiveStringFlags`|Controlla i confronti delle stringhe con distinzione tra maiuscole e minuscole per le impostazioni locali specificate. Per altre informazioni sull'impostazione di questa proprietà, vedere [Proprietà CompareCaseSensitiveStringFlags](https://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx).|  
|`Compression Level`|Se `TransportCompression` è XPRESS, è possibile impostare e quindi controllare il livello di compressione usato. I valori validi sono compresi tra 0 e 9, dove 0 rappresenta la compressione minima e 9 quella massima. Maggiore è la compressione, minori risulteranno le prestazioni. Il valore predefinito è 0.|  
|`Connect Timeout`|Determina la durata massima (in secondi) dei tentativi di connessione da parte del client prima che si verifichi il timeout. Se la connessione non riesce entro il tempo specificato, non vengono effettuati ulteriori tentativi e viene generato un errore.|  
|`MDX Compatibility`|Lo scopo di questa proprietà consiste nell'assicurare un set coerente di comportamenti MDX per le applicazioni che eseguono query MDX. Tramite Excel, in cui si usano query MDX per popolare e calcolare una tabella pivot connessa ad Analysis Services, questa proprietà viene impostata su 1 per garantire che i membri segnaposto in gerarchie incomplete siano visibili nella tabella pivot. I valori validi includono 0,1 e 2.<br /><br /> Con 0 e 1 i membri segnaposto vengono esposti, con 2 no. Un valore vuoto equivale a 0.|  
|`MDX Missing Member Mode=Error`|Indica se i membri mancanti vengono ignorati nelle istruzioni MDX. I valori validi sono Default, Error e Ignore. Per impostazione predefinita, viene usato un valore definito dal server. Con Error viene generato un errore se un membro non esiste. Con Ignore i valori mancanti vengono ignorati.|  
|`Optimize Response`|Maschera di bit indicante quali delle seguenti ottimizzazioni della risposta alle query sono abilitate.<br /><br /> 0x01: Valore predefinito. Usare il NormalTupleSet <br />0x02: Utilizzare questa opzione quando i filtri dei dati sono vuoti|  
|`Packet Size`|Dimensioni di un pacchetto di rete (in byte) comprese tra 512 e 32.767. Le dimensioni predefinite dei pacchetti di rete sono pari a 4096.|  
|`Protocol Format`|Imposta il formato dell'XML inviato al server. I valori validi sono Default, XML o Binary. Il protocollo è XMLA. È possibile specificare che l'XML sia inviato in formato compresso (impostazione predefinita), come XML non elaborato o in un formato binario. Il formato binario codifica attributi ed elementi XML, riducendone le dimensioni. La compressione è un formato proprietario che riduce ulteriormente le dimensioni di richieste e risposte. I formati di compressione e binari sono usati per velocizzare le richieste e le risposte di trasferimento dati.<br /><br /> È necessario usare una libreria client per la connessione se si usano un formato binario o compresso. Il provider OLE DB può creare richieste e risposte in formato binario o compresso. AMO e ADOMD.NET creano le richieste in formato testo, ma accettano risposte in formato binario o compresso.<br /><br /> Questa proprietà della stringa di connessione è equivalente alle impostazioni di configurazione del server `EnableBinaryXML` e `EnableCompression`.|  
|`Real Time Olap`|Impostare questa proprietà per ignorare la memorizzazione nella cache. In questo caso, tutte le partizioni rimangono attivamente in attesa di notifiche di query. Per impostazione predefinita, questa proprietà non è impostata.|  
|`Safety Options`|Imposta il livello di sicurezza per le funzioni e le azioni definite dall'utente. I valori validi sono 0, 1 e 2. In una connessione Excel questa proprietà è Safety Options=2. Dettagli su questa opzione sono disponibili in <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.|  
|`SQLQueryMode`|Specifica se le query SQL includono calcoli. I valori validi sono Data, Calculated e IncludeEmpty. Data indica che non sono consentiti calcoli. Con il valore Calculated sono consentiti calcoli. IncludeEmpty consente la restituzione di calcoli e righe vuote nel risultato della query.|  
|`Timeout`|Specifica la quantità di tempo (in millisecondi) per cui la libreria client attende il completamento di un comando prima di generare un errore.|  
|`Transport Compression`|Definisce la modalità di compressione delle comunicazioni client e server, se la compressione viene specificata tramite la proprietà `Protocol Format`. I valori validi sono Default, None, Compressed e `gzip`. Il valore Default non prevede compressione per TCP mentre il valore `gzip` non la prevede per HTTP. None indica che non viene usata alcuna compressione. Il valore Compressed prevede l'uso della compressione XPRESS (SQL Server 2008 e versioni successive). `gzip` è valido solo per le connessioni HTTP, se la richiesta HTTP include Accept-Encoding = gzip.|  
|`UseExistingFile`|Usata per la connessione a un cubo locale. Questa proprietà specifica se il cubo locale viene sovrascritto. I valori validi sono True o False. Se è impostata su true, il file del cubo deve esistere. Il file esistente sarà la destinazione della connessione. Se impostata su False, il file del cubo viene sovrascritto.|  
|`VisualMode`|Impostare questa proprietà per controllare la modalità di aggregazione dei membri quando si applica la sicurezza delle dimensioni.<br /><br /> Per i dati del cubo visualizzabili da chiunque l'aggregazione di tutti i membri è utile perché sono visibili tutti i valori che contribuiscono al totale. Se tuttavia si applicano filtri o restrizioni alle dimensioni in base all'identità dell'utente, la visualizzazione di un totale basato su tutti i membri (combinando sia valori consentiti che valori con restrizioni in un singolo totale) potrebbe causare confusione o mostrare più informazioni di quante ne dovrebbero essere rivelate.<br /><br /> Per specificare la modalità di aggregazione dei membri in caso di applicazione della sicurezza delle dimensioni, è possibile impostare questa proprietà su True in modo da usare solo in valori consentiti oppure su False per escludere dal totale i valori con restrizioni.<br /><br /> Se impostato nella stringa di connessione, questo valore si applica a livello di cubo o di prospettiva. In un modello è possibile controllare i totali visualizzati a un livello più granulare.<br /><br /> I valori validi sono 0, 1 e 2.<br /><br /> 0 è il valore predefinito. Attualmente, il comportamento predefinito corrisponde a 2, ovvero le aggregazioni includono valori che sono nascosti all'utente.<br /><br /> 1 esclude i valori nascosti dal totale. Si tratta della configurazione predefinita per Excel.<br /><br /> 2 include i valori nascosti nel totale. Si tratta del valore predefinito nel server.<br /><br /> <br /><br /> Gli alias per questa proprietà includono `Visual Total` o `Default MDX Visual Mode`.|  
  
##  <a name="bkmk_reserved"></a> Riservate per utilizzo futuro  
 Le proprietà seguenti sono consentite nelle stringhe di connessione, ma non sono funzionanti nelle versioni correnti di Analysis Services.  
  
-   Authenticated User  
  
-   Cache Authentication  
  
-   Cache Mode (l'uso di questa proprietà è stato esaminato nelle versioni precedenti, pertanto, sebbene esistano articoli di blog che ne consigliano l'impiego, è consigliabile evitare di impostare questa proprietà a meno che non sia indicato dal servizio di supporto tecnico Microsoft).  
  
-   Cache Policy  
  
-   Cache Ratio  
  
-   Cache Ratio2  
  
-   Dynamic Debug Limit  
  
-   Debug Mode  
  
-   Modalità  
  
-   SQLCompatibility  
  
-   Use Formula Cache  
  
##  <a name="bkmk_examples"></a> Esempi di stringhe di connessione  
 Questa sezione illustra la stringa di connessione che verrà probabilmente usato per la configurazione di una connessione di Analysis Services in genere utilizzato nelle applicazioni.  
  
 **Stringa di connessione generica**  
  
 È possibile usare una stringa di connessione come questa se si configura una connessione da Reporting Services.  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Stringa di connessione in Excel**  
  
 Tramite la stringa di connessione predefinita di ADOMD.NET in Excel vengono specificati il provider di dati, il server, il nome del database e la sicurezza integrata di Windows. Il livello di MDX Compatibility è sempre impostato su 1. Sebbene sia possibile modificare il valore per la sessione corrente, MDX Compatibility verrà reimpostato su 1 da Excel alla successiva apertura del file.  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 Per altre informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md) e [autenticazione di dati per Excel Services in SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkId=296350).  
  
##  <a name="bkmk_supportedstrings"></a> Formati di stringa di connessione usati in Analysis Services  
 In questa sezione vengono elencati tutti i formati delle stringhe di connessione supportati da Analysis Services. Fatta eccezione per connessioni ai database PowerPivot, è possibile specificare queste stringhe di connessione in applicazioni che si connettono ad Analysis Services.  
  
 **Connessioni native (o dirette) al server**  
  
 `Data Source=server[:port][\instance]` dove "port" e "\instance" sono facoltativi. Ad esempio, specificando "Zdroj dat Source=Server1" apre una connessione per l'istanza predefinita (e la porta predefinita 2383) su un server denominato "server1".  
  
 "Source data source=Server1:Port1" verrà aperta una connessione a un'istanza di Analysis Services in esecuzione sulla porta "port1" del "server1".  
  
 "Source data source=server1\instance1" verrà aprire una connessione a SQL Browser (sulla porta predefinita 2382), verrà risolva la porta per l'istanza denominata "instance1", quindi aprire la connessione a tale porta di Analysis Services.  
  
 "Source data source=Server1:port1\instance1" verrà aprire una connessione a SQL Browser su "port1", verrà risolva la porta per l'istanza denominata "instance1", quindi aprire la connessione a tale porta di Analysis Services.  
  
 **Connessioni cubi locali (file con estensione cub)**  
  
 `Data Source=<path>`, ad esempio "Source=c:\temp\a.cub Data"  
  
 **Connessioni http(s) a msmdpump.dll**  
  
 `Data Source=<URL>`, dove l'URL è l'indirizzo HTTP o HTTPS alla cartella IIS virtuale che contiene msmdpump.dll. Per altre informazioni, vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md)(Autenticazione di Microsoft Business Intelligence e la delega dell'identità).  
  
 **Connessioni HTTP (s) alle cartelle di lavoro di PowerPivot (file con estensione xlsx, xlsb o xlsm)**  
  
 `Data Source=<URL>`, dove l'URL è il percorso di SharePoint a una cartella di lavoro di PowerPivot pubblicata in una libreria di SharePoint. Ad esempio, "Data Source =<http://localhost/Shared> Documents/Sales.xlsx".  
  
 **Connessioni http(s) a file di connessione BI Semantic Model**  
  
 `Data Source=<URL>` dove l'URL è il percorso di SharePoint al file con estensione bism. Ad esempio, "Data Source =<http://localhost/Shared> Documents/Sales.bism".  
  
 **Connessioni a PowerPivot incorporate**  
  
 `Data Source=$Embedded$` dove $embedded$ è un moniker che si riferisce a un modello dei dati PowerPivot incorporato nella cartella di lavoro. Questa stringa di connessione viene creata e è gestita internamente. Non modificarla. Le stringhe di connessione incorporate vengono risolte dal componente aggiuntivo PowerPivot per Excel nelle workstation client o da istanze di PowerPivot per SharePoint in una farm di SharePoint.  
  
 **Contesto del server locale nelle stored procedure di Analysis Services**  
  
 `Data Source=*`, dove * viene risolto nell'istanza locale.  
  
##  <a name="bkmk_encrypt"></a> Crittografia di stringhe di connessione  
 In[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono crittografate e archiviate le stringhe di connessione usate per la connessione a ognuna delle origini dei dati. Se la connessione a un'origine dei dati richiede un nome utente e una password, è possibile fare in modo che tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] il nome e la password vengano archiviati nella stringa di connessione oppure che vengano richiesti ogni volta che è necessario eseguire una connessione all'origine dei dati. Se si configura [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per la richiesta delle informazioni utente, tali informazioni non devono essere archiviate e crittografate. Se tali informazioni vengono archiviate nella stringa di connessione, devono invece essere crittografate e protette.  
  
 Per crittografare e proteggere le informazioni della stringa di connessione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa Data Protection API. In[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene usata una chiave di crittografia separata per crittografare informazioni della stringa di connessione per ogni database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea questa chiave durante la creazione di un database ed esegue la crittografia delle informazioni della stringa di connessione in base all'account di avvio di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . All'avvio di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] la chiave crittografata per ogni database viene letta, decrittografata e archiviata. In[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene quindi usata la chiave decrittografata appropriata per decrittografare le informazioni della stringa di connessione all'origine dati quando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve connettersi a un'origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Configurare Analysis Services per la delega vincolata Kerberos](configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Provider di dati usati per le connessioni ad Analysis Services](data-providers-used-for-analysis-services-connections.md)   
 [Connettersi ad Analysis Services](connect-to-analysis-services.md)  
  
  
