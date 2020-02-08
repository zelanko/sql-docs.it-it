---
title: Guida di riferimento ai messaggi e agli errori di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7d55050b132a3367ecc495d0afedcad6f0d2351b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71284429"
---
# <a name="integration-services-error-and-message-reference"></a>Guida di riferimento ai messaggi e agli errori di Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Nelle tabelle seguenti vengono riportati gli errori, gli avvisi e i messaggi informativi predefiniti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , elencati in ordine numerico crescente all'interno di ciascuna categoria. Vengono inoltre indicati i codici numerici e nomi simbolici corrispondenti. Ognuno degli errori è definito come campo nella classe <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> nello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> .  
  
 Questo elenco può essere utile quando viene visualizzato un codice di errore privo di descrizione. Al momento, nell'elenco non sono incluse informazioni per la risoluzione dei problemi.  
  
> [!IMPORTANT]  
>  Molti dei messaggi di errore visualizzati quando si utilizza [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] provengono da altri componenti. In questo argomento sono inclusi tutti gli errori generati dai componenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Se l'errore desiderato non è visualizzato nell'elenco, è stato generato da un componente esterno a [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], ad esempio provider OLE DB, altri componenti di database, quali [!INCLUDE[ssDE](../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o altri servizi o componenti, quali il file system, il server SMTP o Microsoft Message Queuing (anche noto come MSMQ) e così via. Per informazioni su questi messaggi di errore esterni, vedere la documentazione specifica del componente.  
  
 In questo elenco sono contenuti i gruppi di messaggi seguenti:  
  
-   [Messaggi di errore (DTS_E_*)](#msgError)  
  
-   [Messaggi di avviso (DTS_W_*)](#msgWarning)  
  
-   [Messaggi informativi (DTS_I_*)](#msgInfo)  
  
-   [Messaggi generali e messaggi di evento (DTS_MSG_*)](#msgGeneral)  
  
-   [Messaggi di operazione riuscita (DTS_S_ *)](#msgSuccess)  
  
-   [Messaggi di errore relativi al componente del flusso di dati (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> messaggi di errore  
 I nomi simbolici dei messaggi di errore di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] iniziano con **DTS_E_** .  
  
|Codice esadecimale|Codice decimale|Nome simbolico|Descrizione|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Sovrascrittura della stored procedure "%1" nella destinazione in corso.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|Il tipo di dati "%1" rilevato nella colonna "%2" non è supportato per "%3". La colonna verrà convertita in DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|Per la colonna "%1" della tabella "%2" in XML Schema non è disponibile un mapping nelle colonne di metadati esterne.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|Impossibile inizializzare una variabile o un oggetto interno. Si tratta di un errore interno del prodotto  che viene restituito quando una variabile dovrebbe avere un valore valido ma non lo ha.|  
|0xC0000032|-1073741773|DTS_E_EXPIRED|Il periodo di valutazione di Integration Services è scaduto.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|Impossibile assegnare un valore negativo a questa proprietà. Questo errore si verifica quando viene assegnato un valore negativo a una proprietà che consente solo valori positivi, come la proprietà COUNT.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Gli indici non possono essere negativi. Questo errore si verifica quando si utilizza un valore negativo come indice per una raccolta.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Nome del server non valido: "%1". Il servizio SSIS non supporta più istanze. Specificare solo il nome del server, anziché "nome server\istanza".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Supporto della finestra di progettazione di Visual Tools for Applications non disponibile. Impossibile eseguire la migrazione per gli script VSA in piattaforme a 64 bit. Utilizzare WOW64 per eseguire la migrazione in piattaforme a 64 bit.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|Errori generati durante l'esecuzione del comando.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|Per eseguire un pacchetto SSIS all'esterno di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] è necessario installare %1 di Integration Services o versione successiva.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|Impossibile trovare la variabile. Questo errore si verifica quando si tenta di recuperare una variabile dalla raccolta Variables in un contenitore durante l'esecuzione del pacchetto e la variabile non esiste. È possibile che il nome della variabile sia stato modificato o che la variabile non sia stata creata.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Errore durante il tentativo di scrittura nella variabile di sola lettura "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Impossibile trovare le directory contenenti i componenti Attività e Attività Flusso di dati. Controllare l'integrità dell'installazione.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|Il nome del pacchetto è troppo lungo. Sono consentiti al massimo 128 caratteri. Abbreviare il nome del pacchetto.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|La descrizione del pacchetto è troppo lunga. Sono consentiti al massimo 1024 caratteri. Abbreviare la descrizione del pacchetto.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|Il valore impostato per la proprietà VersionComments è troppo lungo. Sono consentiti al massimo 1024 caratteri. Provare ad abbreviare il valore di VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|Impossibile trovare l'elemento in una raccolta. Questo errore si verifica quando si tenta di recuperare un elemento da una raccolta in un contenitore durante l'esecuzione del pacchetto e l'elemento non viene trovato.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|Impossibile caricare il pacchetto specificato dal database di SQL Server.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|Il valore assegnato alla variabile non è valido. Questo errore si verifica quando il client o un'attività assegna un oggetto di run-time come valore di una variabile.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Errore durante l'assegnazione dello spazio dei nomi alla variabile. Lo spazio dei nomi "System" è riservato per l'utilizzo nel sistema. Questo errore si verifica quando un componente o un'attività tenta di creare una variabile con spazio dei nomi "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|Impossibile trovare la connessione "%1". Questo errore viene generato dalla raccolta Connections quando non è possibile trovare l'elemento connessione specifico.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|La variabile "%1" è di tipo Integer a 64 bit, condizione non supportata nel sistema operativo in uso. È stato eseguito il cast della variabile nel tipo Integer a 32 bit.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|Tentativo di modifica di un attributo di sola lettura nella variabile "%1". Questo errore si verifica quando un attributo di sola lettura per una variabile viene modificato in fase di esecuzione. Gli attributi di sola lettura possono essere modificati solo in fase di progettazione.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Tentativo non valido di impostare una variabile su un riferimento a un contenitore.  Le variabili non possono fare riferimento a contenitori.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Assegnazione di un valore o di un oggetto non valido alla variabile "%1". Questo errore si verifica quando un valore non è appropriato per le variabili.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|Si sono verificati uno o più errori. Dovrebbero essere presenti errori più specifici prima di questo che descrivono nei dettagli gli errori. Questo messaggio viene utilizzato come valore restituito dalle funzioni che rilevano errori.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Errore durante il recupero o l'impostazione di un valore di matrice. Il tipo "%1" non è consentito. Questo errore si verifica durante il caricamento di una matrice in una variabile.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Tipo non supportato nella matrice. Questo errore si verifica durante il salvataggio di una matrice di tipi non supportati in una variabile.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Errore durante il caricamento del valore "%1" dal nodo "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|Il nodo "%1" non è valido. Questo errore si verifica quando non è possibile completare il salvataggio.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Impossibile caricare l'attività "%1", tipo "%2". Informazioni di contatto per l'attività: "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|L'elemento "%1" non esiste nella raccolta "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|Elemento ObjectData mancante nel blocco XML di un oggetto hosted. Questo errore si verifica quando il parser XML tenta di individuare l'elemento dati per un oggetto e tale elemento non viene trovato.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|Impossibile trovare la variabile "%1". Questo errore si verifica quando si tenta di recuperare una variabile da una raccolta di variabili in un contenitore durante l'esecuzione de pacchetto, ma la variabile non viene trovata.  È possibile che il nome della variabile sia stato modificato o che la variabile non sia stata creata.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|Impossibile eseguire il pacchetto. Contiene attività impossibili da caricare.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|Impossibile caricare l'attività. Informazioni di contatto per l'attività: "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Errore durante il caricamento dell'attività "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Errore durante il caricamento dell'attività. Questo errore si verifica quando il caricamento di un'attività dal nodo XML non riesce.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|%1 non è in grado di scrivere nella cache perché %2 ha già scritto in essa.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Impossibile preparare la cache per i nuovi dati.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Impossibile contrassegnare la cache come contenente dati.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|La cache non è inizializzata e non può essere letta da %1.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Impossibile preparare la cache per fornire dati.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|È in corso la scrittura nella cache da parte di %1. La cache non può essere letta da %2.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|È in corso la lettura della cache da parte di %1. La scrittura nella cache da parte di %2 non è possibile.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|Impossibile caricare l'oggetto di run-time dal nodo XML specificato.  Questo errore si verifica quando si tenta di caricare un pacchetto o un altro oggetto da un nodo XML di tipo non corretto, ad esempio un nodo XML non SSIS.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Impossibile aprire il file di pacchetto "%1" a causa dell'errore 0x%2!8.8X! "%3".  Questo errore si verifica quando si carica un pacchetto e non è possibile aprire o caricare il file in modo corretto nel documento XML. La causa può essere l'impostazione di un nome di file non corretto nella chiamata di LoadPackage oppure il formato non corretto del file XML specificato.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Impossibile caricare il documento XML a causa dell'errore 0x%1!8.8X! "%2". Questo errore si verifica quando si carica un pacchetto e non è possibile aprire o caricare il file in modo corretto nel documento XML.  La causa può essere l'impostazione di un nome di file non corretto per il metodo LoadPackage oppure il formato non corretto del file XML specificato.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Impossibile caricare il documento XML dal file di pacchetto "%1" a causa dell'errore 0x%2!8.8X! "%3".  Questo errore si verifica quando si carica un pacchetto e non è possibile aprire o caricare il file in modo corretto in un documento XML. La causa può essere l'impostazione di un nome di file non corretto per il metodo LoadPackage oppure il formato non corretto del file XML specificato.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Impossibile aprire il file di pacchetto. Questo errore si verifica quando si carica un pacchetto e non è possibile aprire o caricare il file in modo corretto in un documento XML. La causa può essere l'impostazione di un nome di file non corretto per il metodo LoadPackage oppure il formato non corretto del file XML specificato.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Impossibile decodificare un formato binario nel pacchetto.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Impossibile caricare il pacchetto come XML perché il formato XML del pacchetto non è valido. Verrà generato un errore specifico del parser XML.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Errore durante il caricamento da XML. Non è possibile fornire ulteriori informazioni dettagliate sul problema perché non è stato passato un oggetto Events in cui archiviare le informazioni dettagliate sull'errore.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Impossibile creare un'istanza del modello a oggetti documento XML. È possibile che MSXML non sia registrato.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|Impossibile caricare il pacchetto. Questo errore si verifica quando si tenta di caricare un pacchetto di una versione precedente oppure quando il file del pacchetto fa riferimento a un oggetto strutturato non valido.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Impossibile salvare il file del pacchetto.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Impossibile salvare il file di pacchetto "%1". Errore 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|L'oggetto deve ereditare da IDTSName100 ma ciò non avviene.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|Il formato della voce di configurazione "%1" non è corretto. Non inizia con il delimitatore di pacchetto. Delimitatore "\package" non presente.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|Il formato della voce di configurazione "%1" non è corretto. Il problema può essere causato da un delimitatore mancante o da errori di formattazione, come un delimitatore di matrice non valido.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Errore durante l'esportazione del file di configurazione.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|Impossibile modificare la raccolta delle proprietà.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Impossibile salvare il file di configurazione. È possibile che il file sia di sola lettura.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|Proprietà FailPackageOnFailure non applicabile al contenitore del pacchetto.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|Impossibile eseguire l'attività "%1" sull'edizione installata %2 di Integration Services. È necessario utilizzare %3 o una versione successiva.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|Impossibile salvare il codice XML in "%1". È possibile che il file sia di sola lettura.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Impossibile convertire un tipo nella configurazione "%1" per il percorso del pacchetto "%2".  Questo errore si verifica quando non è possibile convertire un valore di configurazione da una stringa al tipo di destinazione appropriato. Controllare il valore di configurazione per assicurarsi che sia possibile convertirlo nel tipo della proprietà o variabile di destinazione.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Errore di configurazione. Avviso generico per tutti i tipi di configurazione. Dovrebbero essere presenti altri avvisi precedenti con maggiori informazioni.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Convalida del pacchetto non riuscita dall'attività ExecutePackage. Impossibile eseguire il pacchetto.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Impossibile creare mutex "%1" con errore 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" già esistente e di proprietà di un altro utente.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Impossibile acquisire mutex "%1" con errore 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Impossibile rilasciare mutex "%1" con errore 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|Il puntatore dell'attività del wrapper non è valido. Il wrapper contiene un puntatore non valido a un'attività.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|Il file eseguibile è stato aggiunto alla raccolta Executables di un altro contenitore. Questo errore si verifica quando un client tenta di aggiungere un file eseguibile in più di una raccolta Executables. È necessario rimuovere il file eseguibile dalla raccolta Executables corrente prima di tentare di aggiungerlo.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|Il tipo di connessione "%1" specificato per la gestione connessione "%2" non è riconosciuto come un tipo valido di gestione connessione. Questo errore viene restituito quando si tenta di creare una gestione connessione per un tipo di connessione sconosciuto. Controllare l'ortografia nel nome del tipo di connessione.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|L'oggetto è stato creato ma il tentativo di aggiungerlo a una raccolta non è riuscito. Questo errore può verificarsi a causa di una condizione di memoria insufficiente.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|Errore durante la creazione di un ambiente ODBC (Open Database Connectivity).|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|Errore durante la creazione di una connessione di database ODBC (Open Database Connectivity).|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|Errore durante il tentativo di attivazione di una connessione ODBC (Open Database Connectivity) con il server di database.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|Il qualificatore è già impostato su questa istanza della gestione connessione. È possibile impostare il qualificatore una sola volta per istanza.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|Il qualificatore non è stato impostato su questa istanza della gestione connessione. L'impostazione del qualificatore è obbligatoria per il completamento dell'inizializzazione.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|La gestione connessione non supporta l'impostazione di qualificatori.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Impossibile clonare la gestione connessione "0x%1" per l'esecuzione out-of-process.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|Il provider di log per SQL Server Profiler non è riuscito a caricare il file pfclnt.dll. Verificare che SQL Server Profiler sia installato.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|Errore dell'infrastruttura di registrazione SSIS con codice 0x%1!8.8X!. Questo errore indica che l'errore di registrazione non è attribuibile a un provider di log specifico.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|Errore del provider di log SSIS "%1" con codice 0x%2!8.8X! (%3).  Questo errore indica un errore di registrazione attribuibile al provider di log specificato.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|Il metodo SaveToSQLServer ha rilevato il codice di errore OLE DB 0x%1!8.8X! (%2).  Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|Il metodo LoadFromSQLServer ha rilevato il codice di errore OLE DB 0x%1!8.8X! (%2).  Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|Il metodo RemoveFromSQLServer ha rilevato il codice di errore OLE DB 0x%1!8.8X! (%2). Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|Il metodo ExistsOnSQLServer ha rilevato il codice di errore OLE DB 0x%1!8.8X! (%2). Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|Impossibile attivare una connessione al database utilizzando la stringa di connessione specificata.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|Durante l'aggiunta di un vincolo di precedenza è stato specificato un file eseguibile From non figlio di questo contenitore.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|Durante l'aggiunta di un vincolo di precedenza è stato specificato un file eseguibile To non figlio di questo contenitore.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|Errore durante il tentativo di integrazione di una connessione ODBC in una transazione. Errore di SQLSetConnectAttr durante l'impostazione dell'attributo SQL_ATTR_ENLIST_IN_DTC.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|La gestione connessione "%1" non acquisirà una connessione perché la proprietà OfflineMode del pacchetto è impostata su TRUE. Non è possibile acquisire connessioni quando la proprietà OfflineMode è TRUE.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|SSIS Runtime non è riuscito ad avviare la transazione distribuita a causa dell'errore 0x%1!8.8X! "%2". Impossibile avviare la transazione DTC. È possibile che il servizio MSDTC non sia in esecuzione.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|Impossibile chiamare il metodo SetQualifier su una gestione connessione durante l'esecuzione del pacchetto. Questo metodo viene utilizzato solo in fase di progettazione.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Per archiviare o modificare pacchetti in SQL Server,è necessario che la versione di SSIS Runtime e del database sia la stessa. L'archiviazione di pacchetti in versioni precedenti non è supportata.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Impossibile convalidare la connessione "%1".|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|Il nome di file "%1" specificato nella connessione non è valido.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Impossibile specificare più nomi di file in una connessione quando la proprietà Retain è impostata su TRUE La stringa di connessione include barre verticali che indicano la presenza di più nomi di file e inoltre la proprietà Retain è impostata su TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|Si è verificato un errore ODBC %1!d!|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|Errore nel vincolo di precedenza tra "%1" e "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Impossibile popolare la raccolta ForEachEnumeratorInfos con oggetti nativi ForEachEnumerator. Codice di errore: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|Errore del metodo GetEnumerator dell'enumeratore ForEach con codice 0x%1!8.8X! "%2". Questo errore si verifica quando l'enumeratore ForEach non è in grado di eseguire l'enumerazione.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|Impossibile ottenere i dati non elaborati del certificato dall'oggetto certificato specificato (errore: %1). Questo errore si verifica quando CPackage::put_CertificateObject non è in grado di creare un'istanza dell'oggetto ManagedHelper, quando si verifica un errore nell'oggetto ManagedHelper oppure quando l'oggetto ManagedHelper restituisce una matrice in formato non corretto.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Impossibile creare il contesto del certificato (errore: %1). Questo errore si verifica in CPackage::put_CertificateObject o CPackage::LoadFromXML quando la funzione CryptoAPI corrispondente ha esito negativo.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Impossibile aprire l'archivio certificati personale. Errore: "%1". Questo errore si verifica in CPackage::LoadUserCertificateByName e CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|Impossibile trovare il certificato specificato in base al nome nell'archivio certificati personale (errore: %1). Questo errore si verifica in CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Impossibile trovare il certificato specificato in base all'hash nell'archivio certificati personale (errore: %1). Questo errore si verifica in CPackage::LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|Il valore hash non è una matrice unidimensionale di byte (errore: %1). Questo errore si verifica in CPackage::LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|Impossibile accedere ai dati nella matrice (errore: %1). Questo errore può verificarsi per ogni chiamata di GetDataFromSafeArray.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|La creazione dell'oggetto helper gestito SSIS non è riuscita con errore: 0x%1!8.8X! "%2". Questo errore si verifica ogni volta che CoCreateInstance CLSID_DTSManagedHelper ha esito negativo.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|SSIS Runtime non è riuscito a integrare la connessione OLE DB in una transazione distribuita con errore 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Impossibile firmare il pacchetto. Errore: 0x%1!8.8X! "%2". Questo errore si verifica in caso di esito negativo del metodo ManagedHelper.SignDocument.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Non è stato possibile controllare la busta della firma XML nel pacchetto XML con errore 0x%1!8.8X! "%2". Questo errore si verifica in CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Impossibile ottenere l'origine XML dall'oggetto DOM XML. Errore 0x%1!8.8X! "%2". Questo errore si verifica in caso di esito negativo di IXMLDOMDocument::get_xml.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|Verifica della firma crittografica del pacchetto non riuscita a causa dell'errore 0x%1!8.8X! "%2". Questo errore si verifica in caso di esito negativo dell'operazione di verifica della firma.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Impossibile ottenere la coppia di chiavi crittografiche associate al certificato specificato. Errore 0x%1!8.8X! "%2". Verificare che sia disponibile la coppia di chiavi per cui è stato rilasciato il certificato. Questo errore si verifica in genere quando si tenta di firmare un documento utilizzando un certificato per il quale non si dispone della chiave privata.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|La firma digitale non è valida. Il contenuto del pacchetto è stato modificato.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|La firma digitale è valida. Tuttavia il firmatario non è attendibile e pertanto non è possibile garantire l'autenticità.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|La connessione non supporta l'integrazione in una transazione distribuita.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Impossibile applicare la protezione del pacchetto. Errore 0x%1!8.8X! "%2". Questo errore si verifica durante il salvataggio in formato XML.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Impossibile rimuovere la protezione del pacchetto. Errore 0x%1!8.8X! "%2". Questo errore si verifica nel metodo CPackage::LoadFromXML.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|Il pacchetto è crittografato con una password. La password non è stata specificata, o non è corretta.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|Esiste già un vincolo di precedenza tra i file eseguibili specificati. Non è consentito più di un vincolo di precedenza.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|Non è possibile caricare il pacchetto a causa dell'errore 0x%1!8.8X! "%2". Questo errore si verifica in caso di esito negativo di CPackage::LoadFromXML non riesce.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Impossibile trovare l'oggetto pacchetto nella busta XML firmata (errore: 0x%1!8.8X! "%2". Questo errore si verifica quando la busta XML firmata non contiene un pacchetto SSIS, come previsto.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|Le lunghezze delle matrici dei nomi, dei tipi e delle descrizioni dei parametri non sono uguali ed è necessario che lo siano. Questo errore si verifica quando le lunghezze delle matrici non corrispondono. Ogni matrice dovrebbe includere una voce per ogni parametro.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|Si è verificato un errore OLE DB 0x%1!8.8X! (%2) durante l'enumerazione dei pacchetti. Impossibile eseguire un'istruzione SQL inoltrata.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|Il tipo di provider di log "%1" specificato per il provider di log "%2" non è riconosciuto come tipo di provider di log valido. Questo errore si verifica quando viene eseguito un tentativo di creazione di un provider di log per un tipo di provider di log sconosciuto. Controllare l'ortografia del nome del tipo di provider di log.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|Il tipo di provider di log non è riconosciuto come tipo di provider di log valido. Questo errore si verifica quando viene eseguito un tentativo di creazione di un provider di log per un tipo di provider di log sconosciuto. Controllare l'ortografia del nome del tipo di provider di log.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|Il tipo di connessione specificato per la gestione connessione non è valido. Questo errore si verifica quando viene eseguito un tentativo di creazione di una gestione connessione per un tipo di connessione sconosciuto. Controllare l'ortografia del nome del tipo di connessione.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|Si è verificato un errore durante il tentativo di rimozione del pacchetto "%1" da SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|Si è verificato un errore durante il tentativo di creazione di una cartella in un'istanza di SQL Server denominata "%1" nella cartella "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|Il metodo CreateFolderOnSQLServer ha rilevato il codice di errore OLE DB 0x%1!8.8X! (%2). Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|Errore durante la ridenominazione della cartella " %1\\\\%2" to "%1\\\\%3" in SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|Il metodo RenameFolderOnSQLServer ha rilevato un errore OLE DB con codice 0x%1!8.8X! (%2). Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Errore durante l'eliminazione della cartella di SQL Server "%1".|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|Il metodo RemoveFolderOnSQLServer ha rilevato un errore OLE DB con codice 0x%1!8.8X! (%2). Impossibile eseguire l'istruzione SQL inoltrata.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|Il percorso del pacchetto specificato non contiene un nome di pacchetto. Questo errore si verifica quando il percorso non contiene almeno una barra rovesciata o una barra.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Impossibile trovare la cartella "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|Durante il tentativo di ricerca di una cartella in SQL si è verificato un errore OLE DB con codice 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|Il provider di log SSIS non è riuscito ad aprire il log. Codice errore: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Impossibile recuperare la raccolta ConnectionInfos. Errore 0x%1!8.8X! "%2". Questo errore si verifica in caso di esito negativo della chiamata a IDTSApplication100::get_ConnectionInfos.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Rilevato deadlock durante il tentativo di blocco delle variabili. Impossibile acquisire blocchi dopo 16 tentativi. Timeout dei blocchi.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|VariableDispenser non ha restituito la raccolta Variables. Tentativo di esecuzione di un'operazione consentita solo per le raccolte rese disponibili per l'accesso in lettura e scrittura.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|Questa raccolta Variables è già stata sbloccata. Il metodo Unlock viene chiamato una sola volta in una raccolta Variables resa disponibile per l'accesso in lettura e scrittura.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|Impossibile sbloccare una o più variabili.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|La raccolta Variables è stata restituita da VariableDispenser e non può essere modificata. Impossibile aggiungere o rimuovere elementi nelle raccolte rese disponibili per l'accesso in lettura e scrittura.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|La variabile "%1" è già inclusa nell'elenco di lettura. È possibile aggiungere una variabile una sola volta all'elenco dei blocchi in lettura o all'elenco dei blocchi in scrittura.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|La variabile "%1" è già inclusa nell'elenco di scrittura. È possibile aggiungere una variabile una sola volta all'elenco dei blocchi in lettura o all'elenco dei blocchi in scrittura.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Impossibile bloccare la variabile "%1" per l'accesso in lettura. Errore 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Impossibile bloccare la variabile "%1" per l'accesso in lettura/scrittura. Errore 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|L'evento personalizzato "%1" è già stato dichiarato con un elenco di parametri diverso. Un'attività sta tentando di dichiarare un evento personalizzato quando un'altra attività lo ha già dichiarato con un elenco di parametri diverso.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|L'attività di origine dell'evento personalizzato "%1" non consente la gestione dell'evento nel pacchetto. L'evento personalizzato è stato dichiarato con AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser ha ricevuto una raccolta Variables non protetta. Impossibile ripetere l'operazione.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|Il metodo GetPackagePath è stato chiamato su ForEachEnumerator ma non è stato specificato alcun percorso di pacchetto ForEachLoop.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|Deadlock rilevato durante il tentativo di blocco della variabile "%1" per l'accesso in lettura. Impossibile acquisire un blocco dopo 16 tentativi. Timeout scaduto.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|Deadlock rilevato durante il tentativo di blocco delle variabili "%1" per l'accesso in lettura/scrittura. Impossibile acquisire un blocco dopo 16 tentativi. Timeout dei blocchi.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|Deadlock rilevato durante il tentativo di blocco delle variabili "%1" per l'accesso in lettura e delle variabili "%2" per l'accesso in lettura/scrittura. Impossibile acquisire un blocco dopo 16 tentativi. Timeout dei blocchi.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|Il livello di protezione del pacchetto richiede una password, ma la proprietà PackagePassword è vuota.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Impossibile decrittografare un nodo XML crittografato perché la password non è stata specificata o non è corretta. Verrà eseguito un tentativo di caricamento del pacchetto senza le informazioni crittografate.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Impossibile decrittografare un pacchetto crittografato con una chiave utente. È possibile che l'operazione sia stata eseguita da un utente diverso da quello che ha crittografato il pacchetto oppure in un computer diverso da quello utilizzato per salvare il pacchetto.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|Impossibile utilizzare il livello di protezione ServerStorage per il salvataggio in questa destinazione. Impossibile verificare che la destinazione supporti funzionalità di archiviazione protetta.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|Metodo LoadFromSQLServer non riuscito.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|Impossibile caricare il pacchetto perché lo stato della firma digitale viola i criteri per le firme. Errore 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|Il pacchetto non è firmato.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|Il provider di log per SQL Server Profiler non è riuscito a caricare il file pfclnt.dll poiché è supportato solo su sistemi a 32 bit.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|Impossibile aggiungere l'oggetto perché nella raccolta esiste già un altro oggetto con lo stesso nome. Utilizzare un nome diverso per risolvere l'errore.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|Impossibile modificare il nome dell'oggetto da "%1" a "%2" perché il nome specificato è già utilizzato da un altro oggetto nella raccolta. Utilizzare un nome diverso per risolvere l'errore.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|Errore durante l'enumerazione delle dipendenze del pacchetto. Per ulteriori informazioni, controllare gli altri messaggi.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|Le impostazioni correnti del pacchetto non sono supportate.  Modificare la proprietà SaveCheckpoints o TransactionOption.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|Impossibile eseguire l'esclusione della transazione.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|L'ID del punto di interruzione specificato esiste già. Questo errore si verifica quando un'attività chiama CreateBreakpoint più volte con lo stesso ID. È possibile creare un punto di interruzione con lo stesso ID più volte se l'attività chiama RemoveBreakpoint per il primo punto di interruzione creato prima di creare il secondo.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|L'ID del punto di interruzione specificato non esiste. Questo errore si verifica quando un'attività fa riferimento a un punto di interruzione che non esiste.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|Impossibile aprire il file "%1" per la scrittura. È possibile che il file sia di sola lettura o che non siano disponibili le autorizzazioni corrette.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|Nessun set di righe di risultati associato all'esecuzione di questa query. Il risultato non è specificato in modo corretto.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|File di dump del debug non generati correttamente. Hresult: 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|L'URL specificato non è valido. Questo errore può verificarsi quando l'URL del server o del proxy è Null oppure in formato non corretto. Un formato URL valido è https://ServerName:Port/ResourcePath oppure https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|L'URL %1 non è valido. Questo errore può verificarsi se si specifica uno schema diverso da http o https oppure se il formato dell'URL non è corretto. Un formato URL valido è https://ServerName:Port/ResourcePath oppure https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Impossibile stabilire la connessione al server %. Questo errore può verificarsi quando il server non esiste oppure le impostazioni del proxy non sono corrette.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|Reimpostazione o interruzione della connessione al server. Riprovare più tardi.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|Tentativo di accesso non riuscito per "%1". Questo errore si verifica quando le credenziali di accesso specificate non sono corrette. Verificare le credenziali di accesso.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|Impossibile risolvere il nome del server specificato nell'URL %1.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Impossibile autenticare il proxy. Questo errore si verifica quando non vengono specificate le credenziali di accesso o le credenziali non sono corrette.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|La risposta ottenuta dal server alla richiesta di certificato SSL non è valida. Impossibile elaborare la richiesta.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|Timeout della richiesta. Questo errore può verificarsi quando il timeout specificato è troppo breve oppure non è possibile attivare una connessione al server o al proxy. Verificare che l'URL del server e del proxy siano corretti.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Certificato client mancante. Questo errore si verifica quando il server si aspetta un certificato client SSL e l'utente fornisce un certificato non valido oppure non fornisce affatto un certificato. Per questa connessione è necessario configurare un certificato client.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|Il server specificato, URL %1, include un reindirizzamento e la richiesta di reindirizzamento non è riuscita.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Autenticazione del server non riuscita. Questo errore si verifica quando non vengono specificate le credenziali di accesso o le credenziali non sono corrette.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|Impossibile elaborare la richiesta. Riprovare più tardi.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|Il server ha restituito il codice di stato - %1!u! : %2. Questo errore si verifica in presenza di problemi nel server.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|Piattaforma non supportata dai servizi WinHttp.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Valore di timeout non valido. Il valore di timeout deve essere compreso nell'intervallo da %1!d! a %2!d! (in secondi).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|Dimensione del blocco non valide. Il valore della proprietà ChunkSize deve essere compreso nell'intervallo da %1!d! a %2!d! (in KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Errore durante l'elaborazione del certificato client. Questo errore può verificarsi quando non è possibile trovare il certificato client specificato nell'archivio certificati personale. Verificare che il certificato client sia valido.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|Il server ha restituito il codice di errore "403 - accesso negato". Questo errore può verificarsi quando la risorsa specificata richiede l'accesso tramite "https", ma il periodo di validità del certificato è scaduto, il certificato non è valido per il tipo di utilizzo richiesto, il certificato è stato revocato oppure non è possibile controllare lo stato di revoca.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Errore durante l'inizializzazione della sessione HTTP con il proxy "%1". Questo errore può verificarsi quando si specifica un proxy non valido. La gestione connessione HTTP supporta solo proxy di tipo CERN.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Errore durante l'apertura dell'archivio certificati.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Impossibile decrittografare il nodo XML protetto "%1". Errore 0x%2!8.8X! "%3". È possibile che non siano disponibili le autorizzazioni necessarie per accedere alle informazioni. Questo errore si verifica in presenza di un errore di crittografia. Verificare che sia disponibile la chiave corretta.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Impossibile decrittografare la stringa di connessione protetta per il server "%1". Errore 0x%2!8.8X! "%3". È possibile che non siano disponibili le autorizzazioni necessarie per accedere alle informazioni. Questo errore si verifica in presenza di un errore di crittografia. Verificare che sia disponibile la chiave corretta.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|Il numero di versione non può essere negativo. Questo errore si verifica quando la proprietà VersionMajor, VersionMinor o VersionBuild del pacchetto è impostata su un valore negativo.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|Durante il caricamento è stata eseguita la migrazione del pacchetto a una versione successiva. Per completare il processo, è necessario ricaricarlo. Questo è un codice di errore interno.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Migrazione del pacchetto da versione% 1! d! alla versione %2!d! non è riuscita con errore 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Impossibile caricare il modulo di migrazione del pacchetto.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Errore del modulo di migrazione del pacchetto.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Impossibile impostare la persistenza predefinita per l'oggetto. Questo errore si verifica quando non è possibile determinare quali oggetti sono inclusi nell'oggetto hosted.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|Impossibile aggiungere o rimuovere un elemento da un pacchetto in modalità run-time. Questo errore si verifica quando viene eseguito un tentativo di aggiunta o rimozione di un oggetto in una raccolta mentre il pacchetto è in esecuzione.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|Impossibile trovare il nodo "%1" nella persistenza predefinita personalizzata. Questo errore si verifica se il nodo XML salvato predefinito di un oggetto estensibile viene modificato in modo da rendere impossibile l'individuazione di un oggetto salvato oppure se viene modificato l'oggetto estensibile.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|Impossibile modificare questa raccolta durante la convalida o l'esecuzione del pacchetto.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|Impossibile modificare la raccolta "%1" durante la convalida o l'esecuzione del pacchetto. Impossibile aggiungere "%2" alla raccolta.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|Impossibile stabilire una connessione al server FTP.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|Errore nell'operazione FTP richiesta. Descrizione dettagliata dell'errore: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|Numero di tentativi non valido. Il numero di tentativi deve essere compreso nell'intervallo da %1!d! e %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|Per il funzionamento della gestione connessione FTP è necessaria la DLL seguente: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|La porta specificata nella stringa di connessione non è valida. Il formato di ConnectionString è ServerName:Port. Il valore Port deve essere un valore Integer compreso nell'intervallo da %1!d! e %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|È in corso la creazione della cartella "%1" ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|È in corso l'eliminazione della cartella "%1" ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Modifica della directory corrente in "%1" in corso. %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|Nessun file da trasferire. Questo errore può verificarsi se si esegue un'operazione di invio o ricezione e non sono specificati file da trasferire.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|Il percorso locale specificato non è valido. Specificare un percorso locale valido. Questo errore può verificarsi quando il percorso locale specificato è Null.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|Nessun file specificato per l'eliminazione.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Errore interno durante il caricamento del certificato. Questo errore può verificarsi quando i dati del certificato non sono validi.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Errore interno durante il salvataggio dei dati del certificato.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|Il file del checkpoint "%1" non corrisponde al pacchetto. L'ID del pacchetto e l'ID nel file del checkpoint non corrispondono.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|È stato individuato un file del checkpoint esistente con contenuto apparentemente non appropriato per questo pacchetto. Impossibile sovrascrivere il file per iniziare il salvataggio di nuovi checkpoint. Rimuovere il file del checkpoint esistente e riprovare. Questo errore si verifica quando esiste un file del checkpoint e il pacchetto è impostato per non utilizzare un file del checkpoint ma per salvare i checkpoint. Il file del checkpoint esistente non verrà sovrascritto.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|Il file del checkpoint "%1" è bloccato da un altro processo. Questo errore può verificarsi se è in esecuzione un'altra istanza del pacchetto.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Impossibile aprire il file del checkpoint "%1" a causa dell'errore 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Non è possibile creare il file del checkpoint "%1" a causa dell'errore 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|Valore non valido per la porta FTP. Il valore della porta FTP deve essere un valore Integer compreso nell'intervallo da %1!d! e %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Impossibile connettersi al servizio SSIS nel computer "%1":<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|La proprietà Expression non è supportata per gli oggetti Variable. Utilizzare la proprietà EvaluateAsExpression in alternativa.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|Impossibile valutare l'espressione "%1" nella proprietà "%2". Modificare l'espressione in modo che sia valida.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|Impossibile scrivere il risultato dell'espressione "%1" nella proprietà "%2". L'espressione è stata valutata ma non è possibile impostarne il risultato nella proprietà.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|L'espressione di valutazione per il ciclo non è valida. È necessario modificare l'espressione. Dovrebbero essere presenti ulteriori messaggi di errore.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|L'espressione "%1" deve restituire True o False. Modificare l'espressione in modo che restituisca un valore booleano.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|Nessuna espressione da valutare per il ciclo. Questo errore si verifica quando l'espressione nel ciclo For è vuota. Aggiungere un'espressione.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|L'espressione assegnata al ciclo non è valida e deve essere modificata. Dovrebbero essere presenti ulteriori messaggi di errore.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|L'espressione di inizializzazione per il ciclo non è valida e deve essere modificata. Dovrebbero essere presenti ulteriori messaggi di errore.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|Il numero di versione del pacchetto non è valido. Il numero di versione non può essere maggiore del numero corrente.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|Il numero di versione del pacchetto non è valido. Il numero di versione è negativo.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|Il formato del pacchetto corrisponde a una versione precedente, ma l'aggiornamento automatico del formato del pacchetto è disabilitato.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|Troncamento durante la valutazione dell'espressione.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|Il wrapper non ha potuto impostare il valore della variabile specificata nella proprietà ExecutionValueVariable.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|Impossibile valutare l'espressione per la variabile "%1". Errore nell'espressione.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|Operazione richiesta non supportata dalla versione di database in uso.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Impossibile specificare una transazione quando si utilizza una connessione mantenuta. Questo errore si verifica quando la proprietà Retain è impostata su TRUE nella gestione connessione, ma è presente una chiamata di AcquireConnection con un parametro non Null per le transazioni.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Contesto di transazione non compatibile specificato per una connessione mantenuta. La connessione è stata stabilita nell'ambito di un contesto di transazione diverso. Le connessioni mantenute possono essere utilizzate in un solo contesto di transazione.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Impossibile riprendere la chiamata perché il pacchetto non è sospeso. Questo errore si verifica quando vengono riprese le chiamate client ma il pacchetto non è sospeso.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Impossibile chiamare Execute perché il file eseguibile è già in esecuzione. Questo errore si verifica quando il client chiama Execute su un contenitore già in esecuzione in seguito all'ultima chiamata Execute.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Impossibile chiamare Suspend o Resume perché il file eseguibile non è in esecuzione oppure non si tratta del file eseguibile di primo livello. Questo errore si verifica quando il client chiama Suspend o Resume su un file eseguibile che non sta già elaborando una chiamata Execute.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|Il file specificato nell'enumeratore For Each File non è valido. Controllare che il file specificato nell'enumeratore For Each File esista.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|L'indice del valore non è un numero intero. È in corso l'esecuzione del mapping di un numero For Each Variable %1!d! alla variabile "%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|L'indice del valore è negativo. È in corso il mapping del numero ForEach Variable %1!d! alla variabile "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|Impossibile applicare il mapping del numero ForEach Variable %1!d! alla variabile "% 2".|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Errore durante l'aggiunta di un oggetto a un ForEachPropertyMapping che non rappresenta un figlio diretto del contenitore ForEachLoop.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Impossibile rimuovere una variabile di sistema. Questo errore si verifica quando si rimuove una variabile obbligatoria.  Le variabili obbligatorie sono variabili create dal runtime per le comunicazioni tra le attività e il runtime.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Impossibile modificare la proprietà di una variabile perché si tratta di una variabile di sistema. Le variabili di sistema sono di sola lettura.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Impossibile modificare il nome di una variabile perché si tratta di una variabile di sistema. Le variabili di sistema sono di sola lettura.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Impossibile modificare lo spazio dei nomi di una variabile perché si tratta di una variabile di sistema. Le variabili di sistema sono di sola lettura.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Impossibile modificare il nome del gestore dell'evento. I nomi dei gestori di eventi sono di sola lettura.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Impossibile recuperare il percorso dell'oggetto. Errore di sistema.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|Il tipo del valore da assegnare alla variabile "%1" è diverso dal tipo corrente della variabile. Non è possibile modificare il tipo delle variabili durante l'esecuzione. I tipi delle variabili sono fissi, ad eccezione delle variabili di tipo Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Caratteri non validi nella stringa: "%1". Questo errore si verifica quando una stringa specificata per un valore di proprietà contiene caratteri non stampabili.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|Il nome dell'oggetto SSIS non è valido. Sono stati generati errori più specifici che descrivono in dettaglio il problema relativo al nome.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|La proprietà "%1"è di sola lettura. Questo errore si verifica quando si tenta di modificare una proprietà di sola lettura.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|L'oggetto non supporta informazioni sul tipo. Questo errore si verifica quando il runtime tenta di recuperare informazioni sul tipo da un oggetto per popolare la raccolta Properties.  L'oggetto deve supportare informazioni sul tipo.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|Errore durante il recupero del valore della proprietà "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|Errore durante il recupero del valore della proprietà "%1". Codice di errore: 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|Errore durante l'impostazione del valore della proprietà "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|Errore durante l'impostazione del valore della proprietà "%1". Codice di errore: 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|La proprietà "%1" è di sola scrittura. Questo errore si verifica quando si tenta di recuperare il valore di una proprietà tramite un oggetto proprietà, ma la proprietà è di sola scrittura.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|L'oggetto non implementa IDispatch. Questo errore si verifica quando un oggetto proprietà o una raccolta di proprietà tenta di accedere a un'interfaccia IDispatch in un oggetto.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Impossibile recuperare la libreria dei tipi dell'oggetto. Questo errore si verifica quando la raccolta Properties tenta di recuperare la libreria dei tipi per un oggetto tramite l'interfaccia IDispatch.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Impossibile creare un'attività da XML per l'attività "%1!s!", tipo "%2!s!" a causa dell'errore 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Impossibile creare un documento XML "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|Errore causato dalla presenza di un mapping di proprietà da una variabile a una proprietà con tipo diverso. Il tipo della proprietà deve corrispondere al tipo della variabile.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Tentativo di impostazione del mapping di proprietà su un tipi di oggetto di destinazione non supportato. Questo errore si verifica quando si passa un tipo di oggetto non supportato a un mapping di proprietà.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Impossibile risolvere un percorso di pacchetto in un oggetto nel pacchetto "%1".  Controllare che il percorso del pacchetto sia valido.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|La proprietà di destinazione per il mapping di proprietà è vuota. Impostare il nome della proprietà di destinazione.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|Impossibile ripristinare almeno un mapping di proprietà.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|Il nome di variabile è ambiguo perché esistono più variabili con tale nome in spazi dei nomi diversi. Specificare un nome qualificato con lo spazio dei nomi per evitare ambiguità.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|Oggetto padre non disponibile per l'oggetto di destinazione in un mapping di proprietà. L'oggetto di destinazione non è un figlio di nessun contenitore di sequenza. È possibile che sia stato rimosso dal pacchetto.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|Mapping di proprietà non valido. Il mapping verrà ignorato.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Errore durante la segnalazione della rimozione di una destinazione ai mapping di proprietà.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|Rilevato mapping di proprietà non valido nel ciclo For Each. Questo errore si verifica quando non è possibile ripristinare il mapping della proprietà ForEach.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|È stata specificata una proprietà di destinazione non valida in un mapping di proprietà. Questo errore si verifica quando in un oggetto di destinazione si specifica una proprietà non disponibile per tale oggetto.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Impossibile creare un'attività da XML. Questo errore si verifica quando il runtime non è in grado di risolvere il nome per creare un'attività. Verificare che il nome sia corretto.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|Impossibile sostituire il file del checkpoint esistente con il file del checkpoint aggiornato. Il checkpoint è stato creato in un file temporaneo, ma la sostituzione del file esistente con il file nuovo non è riuscita.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|Il pacchetto è configurato per eseguire sempre il riavvio da un checkpoint, ma il file del checkpoint non è stato specificato.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|Tentativo di caricamento del file del checkpoint XML "%1" non riuscito con errore 0x%2!8.8X! "%3". Controllare che il nome di file specificato sia corretto e che il file esista.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|Errore del pacchetto durante l'esecuzione. Impossibile caricare il file del checkpoint. Per continuare l'esecuzione del pacchetto è necessario un file del checkpoint. Questo errore si verifica in genere quando la proprietà CheckpointUsage è impostata su ALWAYS, valore che indica che il pacchetto viene sempre riavviato.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|L'espressione della condizione di valutazione nel ciclo For "%1" è vuota. Il ciclo For deve includere un'espressione di valutazione booleana.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|Impossibile convertire il risultato dell'espressione di assegnazione "%1" in un tipo compatibile con la variabile a cui è assegnato.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Errore durante l'utilizzo di una variabile di sola lettura "%1" in un'espressione di assegnazione. Impossibile assegnare il risultato dell'espressione alla variabile perché la variabile è di sola lettura. Scegliere una variabile in scrittura oppure rimuovere l'espressione dalla variabile.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Impossibile valutare l'espressione "%1" perché la variabile "%2" non esiste o non è accessibile in scrittura. Impossibile assegnare il risultato dell'espressione alla variabile perché non è possibile trovarla oppure non è possibile bloccarla per l'accesso in scrittura.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|Il tipo di risultato dell'espressione "%1" è "%2" e non può essere convertito in un tipo supportato.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|Impossibile convertire il risultato dell'espressione "%1" dal tipo "%2" a un tipo supportato. Codice di errore: 0x%3!8.8X!. Si è verificato un errore imprevisto durante il tentativo di conversione del risultato dell'espressione in un tipo supportato dal motore di runtime, anche se la conversione di tipo è supportata.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|Nome dell'oggetto non valido. Impossibile impostare il nome su NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|Nome dell'oggetto non valido. Il nome non può essere vuoto.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|Il nome dell'oggetto "%1" non è valido. Nei nomi non è possibile includere i seguenti caratteri: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|Il nome dell'oggetto "%1" non è valido. I nomi non possono contenere caratteri di controllo che li rendono non stampabili.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|Il nome dell'oggetto "%1" non è valido. I nomi non possono iniziare con uno spazio vuoto.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|Il nome dell'oggetto "%1" non è valido. I nomi non possono finire con uno spazio vuoto.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|Il nome dell'oggetto "%1" non è valido. I nomi devono iniziare con un carattere alfabetico.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|Il nome dell'oggetto "%1" non è valido. Il nome deve iniziare con un carattere alfabetico o con il carattere di sottolineatura "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|Il nome dell'oggetto "%1" non è valido. Il nome deve contenere solo caratteri alfanumerici o caratteri di sottolineatura "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|Il nome dell'oggetto "%1" non è valido. I nomi non possono contenere i seguenti caratteri: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Impossibile caricare la proprietà Value "%1" utilizzando la persistenza predefinita.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|La gestione connessione "%1" non è di tipo "%2".|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" vuota|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Nodo dati non valido nella sezione dell'enumeratore NodeList.|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|Impossibile creare enumeratori.|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|Operazione non riuscita perché la cache è in uso.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|Impossibile modificare la proprietà.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|Aggiornamento del pacchetto non riuscito.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Errore 0x%1!8.8X! durante il caricamento del file del pacchetto "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|Pacchetto non specificato.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|Connessione non specificata.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|Il tipo "%2" della gestione connessione "%1" non è supportato. Sono supportate solo le gestioni connessioni di tipo "FILE" e "OLEDB".|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Errore 0x%1!8.8X! durante il caricamento del file del pacchetto "%3" in un documento XML. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Errore 0x%1!8.8X! durante la preparazione del caricamento del pacchetto. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|Impossibile eseguire il metodo Validate sull'attività. Codice di errore restituito: 0x%1!8.8X! (%2). Il metodo Validate deve essere eseguito correttamente e indicare il risultato tramite un parametro di output.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|Impossibile eseguire il metodo Execute sull'attività. Codice di errore restituito: 0x%1!8.8X! (%2). Il metodo Execute deve essere eseguito correttamente e indicare il risultato tramite un parametro di output.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|Si è verificato un errore nell'attività "%1": 0x%2!8.8X! durante il recupero delle dipendenze. L'errore si è verificato durante il recupero delle dipendenze dalla raccolta di dipendenze dell'attività. È possibile che l'attività abbia implementato una delle interfacce delle dipendenze in modo non corretto.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|Errori durante la convalida dell'attività.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|Il formato della stringa di connessione non è valido. Deve essere composta da uno o più componenti nel formato X=Y e separati da punti e virgola. Questo errore si verifica quando si imposta una stringa di connessione composta da zero componenti per una gestione connessione database.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|I componenti della stringa di connessione non possono contenere punti e virgola non racchiusi tra virgolette. Se il valore deve includere un punto e virgola, racchiudere l'intero valore tra virgolette. Questo errore si verifica quando i valori nella stringa di connessione contengono punti e virgola non racchiusi tra virgolette, ad esempio la proprietà InitialCatalog.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Impossibile convalidare uno o più provider di log. Impossibile eseguire il pacchetto. Il pacchetto non viene eseguito in caso di errori di convalida di un provider di log.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Valore non valido nella matrice.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|Un elemento dell'enumeratore restituito da ForEach Enumerator non implementa l'interfaccia IEnumerator, in contraddizione con l'impostazione della proprietà CollectionEnumerator di ForEach Enumerator.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|L'enumeratore non è riuscito a recuperare l'elemento con indice "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Impossibile trovare la funzione.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Impossibile trovare la funzione.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|L'attività Script ActiveX è stata avviata con un elemento XML non corretto.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Impossibile trovare il gestore.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|Errore durante il tentativo di recupero dei linguaggi di scripting installati nel sistema.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|Errore durante la creazione dell'host di scripting ActiveX. Verificare che l'host di scripting sia installato correttamente.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|Errore durante il tentativo di inizializzazione dell'host di scripting per il linguaggio scelto. Verificare che il linguaggio di scripting selezionato sia installato nel sistema.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|Errore durante l'aggiunta di variabili SSIS nello spazio dei nomi dell'host di scripting. È possibile che l'attività non possa utilizzare variabili SSIS nello script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|Errore irreversibile durante il tentativo di analisi del testo dello script. Verificare che il motore di gestione per il linguaggio scelto sia installato correttamente.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|Il nome di funzione immesso non è valido. Verificare che sia stato specificato un nome di funzione valido.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|Errore durante l'esecuzione dello script. Verificare che il motore di scripting per il linguaggio selezionato sia installato correttamente.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|Errore durante l'aggiunta della libreria dei tipi gestita nell'host di scripting. Verificare che sia installato il runtime DTS 2000.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|L'attività Inserimento bulk è stata avviata con un elemento XML non corretto.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Nome del file di dati non specificato.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Impossibile trovare il gestore.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Impossibile acquisire la connessione specificata: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Tentativo di ottenere la gestione connessione non riuscito.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|Connessione non valida.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|Connessione Null.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Esecuzione non riuscita.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|Errore durante il recupero delle tabelle dal database.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|Errore durante il recupero delle colonne della tabella.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|Errore nell'operazione sul database.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|La connessione specificata "%1" non è valida o punta a un oggetto non valido. Per continuare, specificare una connessione valida.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|La connessione di destinazione specificata non è valida. Specificare una connessione valida per continuare.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|È necessario specificare un nome di tabella per continuare.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Errore in LoadFromXML in corrispondenza del tag "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Errore in SaveToXML in corrispondenza del tag "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|Connessione non valida.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Esecuzione non riuscita.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Errore durante il recupero delle tabelle dal database.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Errore durante il recupero delle colonne della tabella.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Errore durante il tentativo di apertura del file di dati.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Impossibile convertire il file OEM di input nel formato specificato.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Errore nell'operazione sul database.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|Nessuna gestione connessione specificata.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|La connessione "%1" non è una connessione di Analysis Services.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Impossibile individuare la connessione "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|L'attività Esegui DDL Analysis Services ha ricevuto un nodo dati di attività non valido.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|L'attività Elaborazione Analysis Services ha ricevuto un nodo dati di attività non valido.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|Istruzioni DDL non valide.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|Le istruzioni DDL in ProcessingCommands non sono valide.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|Impossibile salvare il risultato dell'esecuzione in una variabile di sola lettura.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|La variabile "%1" non è definita.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|La gestione connessione "%1" non è definita.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|La gestione connessione "%1" non è una gestione connessione file.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|Impossibile trovare "%1" durante la deserializzazione.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|Traccia arrestata a causa di un'eccezione.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Esecuzione delle istruzioni DDL non riuscita.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|Nessun file associato alla connessione "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|La variabile "%1" non è definita.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|La connessione file "%1" non è definita.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|L'attività Esegui pacchetto DTS 2000 è stata avviata con un elemento XML non corretto.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Impossibile trovare il gestore.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Nome del pacchetto non specificato.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|ID del pacchetto non specificato.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|GUID di versione del pacchetto non specificato.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server non specificato.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|Nome utente di SQL Server non specificato.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Nome del file di archiviazione non specificato.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|La proprietà pacchetto DTS 2000 è vuota.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|Errore durante l'esecuzione del pacchetto DTS 2000.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Impossibile caricare l'elenco dei computer SQL Server disponibili dalla rete. Controllare la connessione alla rete.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|Il tipo di dati non può essere Null. Specificare il tipo di dati corretto da utilizzare per convalidare il valore.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Impossibile convalidare un valore Null sulla base di qualsiasi tipo di dati.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|Un argomento obbligatorio è Null.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|Per eseguire l'attività Esegui pacchetto DTS 2000, avviare il programma di installazione di SQL Server e utilizzare il pulsante Avanzate nella pagina Componenti da installare per selezionare Componenti legacy.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" non è un tipo di valore.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|Impossibile convertire "%1" in "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|Impossibile convalidare "%1" sulla base di "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Errore in LoadFromXML in corrispondenza del tag "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Errore in SaveToXML in corrispondenza del tag "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|Il valore di timeout specificato non è valido. Specificare il numero di secondi consentiti per l'esecuzione del processo. Il timeout minimo è 0, che indica l'assenza di un valore di timeout ovvero che l'esecuzione del processo continua fino al completamento o fino a quando non si verificano errori. Il valore di timeout massimo è 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Impossibile reindirizzare i flussi se l'esecuzione del processo può continuare oltre la durata dell'attività.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|Timeout del processo.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|File eseguibile non specificato.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|La variabile di output standard è di sola lettura.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|La variabile di errore standard è di sola lettura.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|L'attività Esegui processo ha ricevuto un nodo dati di attività non valido.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|Durante l'esecuzione di "%2" "%3" in "%1", il codice di uscita del processo è stato "%4" mentre era previsto il codice "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|La directory "%1" non esiste.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|Il file o il processo "%1" non esiste nella directory "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|Impossibile trovare il file/processo "%1" nel percorso.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|La directory di lavoro "%1" non esiste.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|Processo terminato con codice restituito "%1". Tuttavia, era previsto il codice "%2".|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Errore dell'oggetto di sincronizzazione.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|L'attività File system ha ricevuto un nodo dati di attività non valido.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|Directory già esistente.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" non valido per il tipo di operazione "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|Proprietà di destinazione dell'operazione "%1" non impostata.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|Proprietà di origine dell'operazione "%1" non impostata.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|Il tipo di connessione "%1" non è un file.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|La variabile "%1" non esiste.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|La variabile "%1" non è una stringa.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|Il file o la directory "%1" rappresentato dalla connessione "%2" non esiste.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|La gestione connessione file di destinazione "%1" ha un tipo di utilizzo non valido: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|La gestione connessione file di origine "%1" ha un tipo di utilizzo non valido: "%2".|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Fornisce informazioni sulle operazioni dell'attività File system.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|Attività File system|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Eseguire operazioni correlate al file system, ad esempio la copia e l'eliminazione di file.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Errore dell'oggetto di sincronizzazione.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Impossibile ottenere l'elenco dei file.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|Il percorso locale è vuoto.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|Il percorso remoto è vuoto.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|La variabile locale è vuota.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|La variabile remota è vuota.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|L'attività FTP ha ricevuto un nodo dati di attività non valido.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|La connessione è vuota. Verificare che venga specificata una connessione FTP valida.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|La connessione specificata non è una connessione FTP. Verificare che venga specificata una connessione FTP valida.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Impossibile inizializzare l'attività su un elemento XML Null.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Impossibile salvare l'attività in un documento XML Null.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Errore in LoadFromXML in corrispondenza del tag "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|Nessun file in "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|La variabile "%1" è vuota.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|La variabile "%1" è vuota.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|Il file "%1" non contiene percorsi di file.|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|La variabile "%1" non contiene percorsi di file.|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|La variabile "%1" non è una stringa.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|La variabile "%1" non esiste.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Percorso non valido nell'operazione "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" esiste già.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|Il tipo di connessione "%1" non è un file.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|Il file rappresentato da "%1" non esiste.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Directory non specificata nella variabile "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|Impossibile trovare file in "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Directory non specificata nella gestione connessione file "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Impossibile eliminare il file locale "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Impossibile rimuovere la directory locale "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Impossibile creare la directory locale "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Impossibile ricevere file con "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Impossibile inviare file con "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Impossibile creare la directory remota con "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Impossibile rimuovere la directory remota con "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Impossibile eliminare i file remoti con "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Impossibile connettersi al server FTP con "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|La variabile "%1" non inizia con "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|Il percorso remoto "%1" non inizia con "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|Errore durante l'acquisizione della connessione FTP. Verificare che sia stato specificato un tipo di connessione valido "%1".|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Impossibile aprire l'archivio certificati.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|Errore durante il recupero del nome visualizzato del certificato.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|Errore durante il recupero del nome dell'autorità emittente del certificato.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|Errore durante il recupero del nome descrittivo del certificato.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|Nome della connessione MSMQ non impostato.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|L'attività è stata inizializzata su un elemento XML non corretto.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|Nome del file di dati vuoto.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|Il nome specificato per il file di dati da salvare è vuoto.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|Le dimensioni del file devono essere inferiori a 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Salvataggio del file di dati non riuscito.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|La stringa di confronto è vuota.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Percorso della coda non valido.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|L'attività Message Queue non supporta l'integrazione in transazioni distribuite.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|Tipo di messaggio non valido.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|Timeout della coda di messaggi. Non è stato ricevuto alcun messaggio.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|La proprietà specificata non è valida. Verificare che il tipo dell'argomento sia valido.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Messaggio non autenticato.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|Si sta tentando di impostare il valore di Algoritmo di crittografia con un oggetto non valido.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|La variabile per la ricezione del messaggio stringa è vuota.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|La variabile per la ricezione del messaggio variabili è vuota.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|La connessione "%1" non è di tipo MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|File di dati "%1" già esistente nel percorso specificato. Impossibile sovrascrivere il file. L'opzione di sovrascrittura è impostata su False.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|Impossibile trovare nella raccolta delle variabili del pacchetto la variabile specificata "%1" per la ricezione del messaggio stringa.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|La gestione connessione "%1" è vuota.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|La gestione connessione "%1" non esiste.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Errore "%1": "%2"\r\nRiga "%3"   Colonne da "%4" a "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|Errore durante la compilazione dello script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Errore "%1": "%2"\r\nRiga "%3" Colonne "%4"-"%5"\r\nTesto riga: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|Lo script dell'utente ha restituito un errore come risultato.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|Impossibile caricare i file script dell'utente.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|Lo script dell'utente ha generato un'eccezione: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Impossibile creare un'istanza della classe EntryPoint "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|Eccezione durante il caricamento dell'attività Script dal file XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|Impossibile trovare l'elemento di origine "%1" nel pacchetto.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|Impossibile trovare l'elemento binario "%1" nel pacchetto.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" non è stato riconosciuto come linguaggio di scripting valido.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|Nome dello script non valido. Non può contenere spazi, barre o caratteri speciali né iniziare con un numero.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|Il linguaggio di scripting specificato non è valido.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Impossibile eseguire l'inizializzazione su un'attività Null.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|L'interfaccia utente dell'attività Script deve essere inizializzata su un'attività Script.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|L'interfaccia utente dell'attività Script non è inizializzata.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|Il nome non può essere vuoto.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|Nome del progetto non valido. Non può contenere spazi, barre o caratteri speciali né iniziare con un numero.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|Il linguaggio di scripting specificato non è valido.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Impossibile trovare il punto di ingresso.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|Il linguaggio di scripting non è stato specificato. Specificare un linguaggio di scripting valido.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|Inizializzazione interfaccia utente: attività Null.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|L'interfaccia utente dell'attività Script è inizializzata su un'attività non corretta.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|Nessun destinatario specificato.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|Server SMTP (Simple Mail Transfer Protocol) non specificato. Specificare un nome o un indirizzo IP valido per il server SMTP.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Attività Invia messaggi inizializzata su un elemento XML non corretto.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|Il file "%1" non esiste oppure non si dispone delle autorizzazioni necessarie per accedere al file.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Verificare che il server SMTP (Simple Mail Transfer Protocol) specificato sia valido.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|La connessione "%1" non è di tipo File.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|Nell'operazione "%1", il file "%2" non esiste.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|La variabile "%1" non è di tipo string.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|La connessione "%1" non è di tipo SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|La connessione "%1" è vuota.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|La connessione specificata "%1" non esiste.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|Nessuna istruzione Transact-SQL specificata.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|La connessione non supporta set dei risultati XML.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Impossibile individuare un gestore per il tipo di connessione specificato.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|Nessuna gestione connessione specificata.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Impossibile acquisire una connessione dalla gestione connessione.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Nomi di parametro Null non supportati.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|Nome del parametro non valido.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|I nomi di parametro validi sono di tipo int o string.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|Impossibile utilizzare la variabile "%1" in un'associazione di risultati. È di sola lettura.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|Indice non assegnato a questa raccolta.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|Impossibile utilizzare la variabile "%1" come parametro di output o come valore restituito in un'associazione di parametri. La variabile è di sola lettura.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|L'oggetto non esiste nella raccolta.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Impossibile acquisire una connessione gestita.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Impossibile popolare le colonne di risultati per un tipo di risultato a riga singola. La query ha restituito un set di risultati vuoto.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|Numero non valido di associazioni di risultati restituiti per ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|Il nome dell'associazione di risultati deve essere impostato su zero per set dei risultati completi e risultati XML.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|Flag di direzione del parametro non valido.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|Il frammento XML non contiene dati dell'attività SQL.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|Il primo parametro non è un parametro con valore restituito relativo al tipo oppure sono disponibili più parametri con valore restituito relativo al tipo.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|La connessione "%1" non è una gestione connessione file.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|Il file rappresentato da "%1" non esiste.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|La variabile "%1" non è di tipo string.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|La variabile "%1" non esiste o non è possibile bloccarla.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|La gestione connessione "%1" non esiste.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Impossibile acquisire la connessione "%1". È possibile che la connessione non sia configurata correttamente oppure che non siano disponibili le autorizzazioni appropriate per la connessione.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|L'associazione di risultati in base al nome "%1" non è supportata per questo tipo di connessione.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|È stato specificato il tipo di set di risultati a riga singola, ma non è stata restituita alcuna riga.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|Nessun recordset disconnesso disponibile per l'istruzione Transact-SQL.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Tipo non supportato.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Tipo sconosciuto.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Tipo di dati non supportato nell'associazione di parametro \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|I nomi di parametro non possono essere costituiti da una combinazione di numeri ordinali e tipi denominati.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|Direzione del parametro non valida nell'associazione di parametro \\"%s\\".|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|Tipo di dati non supportato nell'associazione del set dei risultati \\"%s\\".|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|Indice di colonna del risultato %d non valido.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Impossibile trovare la colonna \\"%s\\" nel set dei risultati.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|Nessun set di righe di risultati associato all'esecuzione di questa query.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|recordset disconnessi non disponibili da connessioni ODBC.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|Il tipo di dati nella colonna %hd del set dei risultati non è supportato.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|Impossibile caricare il documento XML con i risultati della query.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|È necessario specificare un nome di connessione o di variabile per il pacchetto.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Impossibile creare il pacchetto.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|TableMetaDataNode non è un oggetto XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Impossibile creare la pipeline.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|La variabile non è del tipo corretto.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|La gestione connessione specificata non è una gestione connessione file.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Nome di file non valido specificato nella gestione connessione "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|La connessione è vuota. Specificare una connessione HTTP valida.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|La connessione non esiste. Specificare una connessione HTTP esistente valida.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|La connessione specificata non è una connessione HTTPHTTP. Specificare una connessione HTTP valida.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|Nome del servizio Web vuoto. Specificare un nome di servizio Web valido.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|Nome del metodo Web vuoto. Specificare un nome di metodo Web valido.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|Nome del metodo Web vuoto o inesistente. Specificare un nome di metodo Web esistente.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|Percorso di output vuoto. Specificare una variabile o una connessione file esistente.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|Impossibile trovare la variabile. Verificare che la variabile esista nel pacchetto.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Impossibile salvare il risultato. Verificare che la variabile non sia di sola lettura.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Errore in LoadFromXML in corrispondenza del tag "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Errore in SaveToXML in corrispondenza del tag "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Impossibile salvare l'attività in un documento XML Null.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Impossibile inizializzare l'attività su un elemento XML Null.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|L'attività Servizio Web è stata avviata con un elemento XML non corretto.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Trovato elemento XML imprevisto.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|Errore durante l'acquisizione della connessione HTTP. Specificare un tipo di connessione valido.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Impossibile salvare il risultato. Verificare che sia disponibile una connessione file esistente.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Impossibile salvare il risultato. Verificare che il file esista.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Impossibile salvare il risultato. Il nome del file è vuoto o il file è utilizzato da un altro processo.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|Errore durante l'acquisizione della connessione file. Specificare una connessione file valida.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Sono supportati solo tipi complessi con valori primitivi, matrici di primitive ed enumerazioni.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Sono supportati solo tipi Primitive, Enum, Complex, PrimitiveArray e ComplexArray.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|Versione di WSDL non supportata.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Inizializzazione eseguita su un elemento XML non corretto.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|Impossibile trovare un attributo obbligatorio.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|L'enumerazione "%1" non contiene valori. Il codice WSDL è danneggiato.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|Impossibile trovare la connessione.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Esiste già una connessione con questo nome.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|La connessione non può essere Null o vuota.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|La connessione specificata non è una connessione HTTPHTTP. Specificare una connessione HTTP valida.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|L'URI (Uniform Resource Identifier) specificato non contiene una descrizione WSDL valida.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Impossibile leggere il file WSDL. File WSDL di input non valido. Il lettore ha generato l'errore seguente: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|La descrizione del servizio non può essere Null.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|Il nome del servizio non può essere Null.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|L'URL non può essere Null.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|Il servizio attualmente non è disponibile.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|Servizio non disponibile sulla porta SOAP.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Impossibile analizzare il file WSDL. Impossibile trovare l'associazione corrispondente alla porta SOAP.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Impossibile analizzare il file WSDL. Impossibile trovare un PortType corrispondente alla porta SOAP.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Impossibile trovare il messaggio corrispondente al metodo specificato.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Impossibile generare il proxy per il servizio Web specificato. Durante la generazione del proxy sono stati rilevati gli errori seguenti "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Impossibile caricare il proxy per il servizio Web specificato. L'errore esatto è il seguente: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Impossibile trovare il servizio specificato. L'errore esatto è il seguente: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|Il servizio Web ha generato l'errore seguente durante l'esecuzione del metodo: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Impossibile eseguire il metodo Web. L'errore esatto è il seguente: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo non può essere Null.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|Il valore WebMethodInfo non è corretto. Il valore ParamValue specificato non corrisponde al ParamType. Il valore DTSParamValue non è di tipo PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|Il valore WebMethodInfo specificato non è corretto. Il valore ParamValue specificato non corrisponde al ParamType. Il valore DTSParamValue rilevato non è di tipo EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|Il valore WebMethodInfo specificato non è corretto. Il valore ParamValue specificato non corrisponde al ParamType. DTSParamValue trovato non è di tipo ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|Il valore WebMethodInfo specificato non è corretto. Il valore ParamValue specificato non corrisponde al ParamType. Il valore DTSParamValue rilevato non è di tipo ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|Il valore WebMethodInfo specificato non è corretto. "%1" non è di tipo Primitive.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|Formato di ArrayValue non valido. La matrice deve contenere almeno un elemento.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|Il valore dell'enumerazione non può essere Null. Selezionare un valore predefinito per l'enumerazione.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Impossibile convalidare un valore Null sulla base di qualsiasi tipo di dati.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|Il valore dell'enumerazione non è corretto.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|La classe specificata non contiene una proprietà pubblica denominata "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|Impossibile convertire "%1" in "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Impossibile completare la pulizia. È possibile che il proxy creato per il servizio Web non sia stato eliminato.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Impossibile creare un oggetto di tipo "%1". Verificare se esiste il costruttore predefinito.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" non è un tipo di valore.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|Impossibile convalidare "%1" sulla base di "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|Il tipo di dati non può essere Null. Specificare il valore del tipo di dati da convalidare.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|Impossibile inserire ParamValue in questa posizione. L'indice specificato potrebbe essere minore di zero o maggiore della lunghezza.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|File WSDL di input non valido.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Errore dell'oggetto di sincronizzazione.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|Query WQL mancante.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|È necessario impostare la destinazione.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|Nessuna connessione WMI impostata.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|L'attività Lettore di dati WMI ha ricevuto un nodo dati di attività non valido.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|Impossibile convalidare l'attività.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|Il file "%1" non esiste.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|La gestione connessione "%1" non esiste.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|La variabile "%1" non è di tipo string o object.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|La connessione "%1" non è di tipo "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|La connessione "%1" non è di tipo "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|Il file "%1" esiste già.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|La gestione connessione "%1" è vuota.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|La variabile "%1" deve essere di tipo object perché le venga assegnata una tabella di dati.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Attività non riuscita a causa di una query WMI non valida: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Impossibile scrivere nella variabile "%1" perché è impostata per mantenere il valore originale.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Errore dell'oggetto di sincronizzazione.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|Query WQL mancante.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|Connessione WMI mancante.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|Impossibile eseguire la query WMI.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|L'attività Monitoraggio eventi WMI ha ricevuto un nodo dati di attività non valido.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|La gestione connessione "%1" non esiste.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|Il file "%1" non esiste.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|La variabile "%1" non è di tipo string.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|La connessione "%1" non è di tipo "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|La connessione "%1" non è di tipo "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|Il file "%1" esiste già.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|La gestione connessione "%1" è vuota.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Il timeout di "%1" secondi si è verificato prima dell'evento rappresentato da "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Il monitoraggio della query WQL ha causato l'eccezione di sistema seguente: "%1". Controllare la query per correggere eventuali errori oppure controllare i diritti o le autorizzazioni di accesso per la connessione WMI.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|Operazione specificata non definita.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|Il tipo della connessione non è File.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Impossibile ottenere un XmlReader dal documento XML di origine.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Impossibile ottenere un XmlReader dal documento XML modificato.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Impossibile ottenere il lettore di diffgram XDL dal documento XML del diffgram XDL.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|L'elenco dei nodi è vuoto.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|Impossibile trovare l'elemento.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|Operazione specificata non definita.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Elemento di contenuto imprevisto in XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|Impossibile trovare uno schema per applicare la convalida.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|Errore di convalida durante la convalida del documento dell'istanza.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Errore dell'oggetto di sincronizzazione.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|I nodi radice non corrispondono.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|Il tipo di operazione script di modifica nello script di modifica finale non è valido.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|I nodi CDATA devono essere aggiunti con la classe DiffgramAddSubtrees.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|I nodi di commento devono essere aggiunti con la classe DiffgramAddSubtrees.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|I nodi di testo devono essere aggiunti con la classe DiffgramAddSubtrees.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|I nodi con un numero significativo di spazi vuoti devono essere aggiunti con la classe DiffgramAddSubtrees.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Correggere la matrice OperationCost in modo che rifletta l'enumerazione XmlDiffOperation.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|Nessuna operazione nell'attività.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|Il documento contiene già dati e non deve essere riutilizzato.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|Il tipo di nodo non è valido.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|L'attività XML ha ricevuto un nodo dati di attività non valido.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|Il tipo di dati della variabile non è String.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Impossibile recuperare la codifica da XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|Origine non specificata.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|Secondo operando non specificato.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Diffgram XDL non valido. "%1" è un descrittore di percorso non valido.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Diffgram XDL non valido. Nessun nodo corrisponde al descrittore di percorso "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Diffgram XDL non valido. Previsto xd:xmldiff come elemento radice con URI dello spazio dei nomi "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|Diffgram XDL non valido. Attributo srcDocHash mancante nell'elemento xd:xmldiff.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|Diffgram XDL non valido. Attributo options mancante nell'elemento xd:xmldiff.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|Diffgram XDL non valido. Valore non valido per l'attributo srcDocHash.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|Diffgram XDL non valido. Valore non valido per l'attributo options.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|Diffgram XDL non applicabile al documento XML. Valore rcDocHash non corrispondente.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Diffgram XDL non valido. Più nodi corrispondono al descrittore di percorso "%1" nell'elemento xd:node o xd:change.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|Diffgram XDL non applicabile al documento XML. Impossibile aggiungere una nuova dichiarazione XML.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Errore interno. XmlDiffPathSingleNodeList può contenere solo un nodo.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Errore interno. Restano "%1" nodi dopo l'applicazione della patch mentre ne era previsto 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|Il file/testo prodotto da XSLT non è un XmlDocument valido. Impossibile impostarlo come risultato dell'operazione: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|Nessun file associato alla connessione "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|La proprietà "%1" non ha testo XML di origine. Il testo XML non è valido, è Null o è una stringa vuota.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|Il file "%1" esiste già.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|È necessario specificare una connessione di origine.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|È necessario specificare una connessione di destinazione.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|Impossibile trovare la connessione "%1" nel pacchetto.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|La connessione "%1" specifica un'istanza di SQL Server con una versione non supportata per il trasferimento.  Sono supportate solo le versioni 7, 2000 e 2005.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|Per la connessione di origine "%1" è necessario specificare un'istanza di SQL Server con una versione precedente o uguale a quella della connessione di destinazione "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|È necessario specificare un database di origine.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|Il database di origine "%1" deve esistere nel server di origine.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|È necessario specificare un database di destinazione.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|Il database di origine non può essere uguale al database di destinazione.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|Nome di file mancante nelle informazioni per il trasferimento di file %1.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|Cartella mancante nelle informazioni per il trasferimento di file %1.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|Condivisione di rete mancante nelle informazioni per il trasferimento di file %1.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|Il numero di file di origine per il trasferimento deve essere uguale al numero di file di destinazione.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|L'integrazione in transazioni non è supportata.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|Si è verificata l'eccezione seguente durante un trasferimento di database offline: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|Impossibile trovare la condivisione di rete "%1".|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|Impossibile accedere alla condivisione di rete "%1".  Errore: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|L'utente "%1" deve essere un DBO o un sysadmin per "%2" per poter eseguire un trasferimento di database online.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|L'utente "%1" deve essere un sysadmin in "%2" per poter eseguire un trasferimento di database offline.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|È possibile includere cataloghi full-text solo per l'esecuzione di un trasferimento di database offline tra due computer SQL Server 2005.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|Il database "%1" esiste già nel server di destinazione "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|È necessario specificare almeno un file di origine.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Impossibile trovare il file "%1" nel database di origine "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|L'operazione richiesta non è consentita in sistemi conformi con lo standard U.S. FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Esecuzione della query non riuscita con l'errore seguente: "%2". Possibili cause: problemi nella query, impostazione non corretta della proprietà "ResultSet", parametri non impostati correttamente o problemi di attivazione della connessione.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Errore durante la lettura dei nomi delle stored procedure dal file XML.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Nodo dati non valido per l'attività Trasferisci stored procedure.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|La connessione "%1" non è di tipo "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Esecuzione non riuscita con l'errore seguente: "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|Si è verificato un errore con il messaggio di errore seguente: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Esecuzione dell'inserimento bulk non riuscita.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Percorso di destinazione non valido.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Impossibile creare la directory. È stata impostata l'interruzione dell'operazione in caso di directory già esistente.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|L'attività è impostata per l'esecuzione come transazione e la connessione "%1" è di tipo "ODBC". Le connessioni ODBC non supportano transazioni.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|Errore durante l'assegnazione di un valore alla variabile "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|L'origine è vuota.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|La destinazione è vuota.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|Il file o la directory "%1" non esiste.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|La variabile "%1" è utilizzata come origine o destinazione ed è vuota.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|Il file o la directory "%1" è stato eliminato.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|La directory "%1" è stata eliminata.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|La variabile "%1" deve essere di tipo object perché le venga assegnata una tabella di dati.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|La variabile "%1" non ha un tipo di dati string.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|Errore durante l'acquisizione della connessione FTP. Specificare un tipo di connessione valido in "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|Impossibile trovare la gestione connessione FTP "%1".|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|Il tipo di utilizzo file della connessione "%1" deve essere "%2" per l'operazione "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|Il server di origine non può essere uguale al server di destinazione.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|Nessun messaggio di errore da trasferire.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|Dimensioni diverse per gli elenchi di messaggi di errore e delle lingue corrispondenti.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|L'ID del messaggio di errore "%1" non è compreso nell'intervallo consentito per i messaggi di errore definiti dall'utente. Gli ID dei messaggi di errore definiti dall'utente devono essere compresi tra 50000 e 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|Impossibile inserire l'attività una transazione.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Impossibile trasferire alcuni o tutti i messaggi di errore.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|Il messaggio di errore "%1" esiste già nel server di destinazione.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|Impossibile trovare il messaggio di errore "%1" nel server di origine.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Esecuzione non riuscita con l'errore seguente: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Impossibile trasferire il processo o i processi.|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|Nessun processo da trasferire.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|Il processo "%1" esiste già nel server di destinazione.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|Impossibile trovare il processo "%1" nel server di origine.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|L'elenco degli account di accesso da trasferire è vuoto.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Impossibile ottenere l'elenco di account di accesso dal server di origine.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|L'account di accesso "%1" esiste già nel server di destinazione.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|L'account di accesso "%1" non esiste nell'origine.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Impossibile trasferire alcuni o tutti gli account di accesso.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Impossibile trasferire la stored procedure o le stored procedure. Dovrebbe essere stato generato un errore con maggiori informazioni.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Impossibile trovare la stored procedure "%1" nell'origine.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|La stored procedure "%1" esiste già nel server di destinazione.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|Nessuna stored procedure da trasferire.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Impossibile trasferire l'oggetto o gli oggetti.|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|L'elenco degli oggetti da trasferire è vuoto.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|La stored procedure "%1" non esiste nell'origine.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|La stored procedure "%1" esiste già nella destinazione.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di stored procedure da trasferire: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|La regola "%1" non esiste nell'origine.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|La regola "%1" esiste già nella destinazione.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di regole da trasferire: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|La tabella "%1" non esiste nell'origine.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|La tabella "%1" esiste già nella destinazione.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di tabelle da trasferire: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|La vista "%1" non esiste nell'origine.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|La vista "%1" esiste già nella destinazione.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di viste da trasferire: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|La funzione definita dall'utente "%1" non esiste nell'origine.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|La funzione definita dall'utente "%1" esiste già nella destinazione.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di funzioni definite dall'utente da trasferire: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|Il valore predefinito "%1" non esiste nell'origine.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Il valore predefinito "%1" esiste già nella destinazione.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di valori predefiniti da trasferire: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|Il tipo di dati definito dall'utente "%1" non esiste nell'origine.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|Il tipo di dati definito dall'utente "%1" esiste già nella destinazione.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di tipi di dati definiti dall'utente da trasferire: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|La funzione di partizione "%1" non esiste nell'origine.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|La funzione di partizione "%1" esiste già nella destinazione.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di funzioni di partizione da trasferire: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|Lo schema di partizione "%1" non esiste nell'origine.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|Lo schema di partizione "%1" esiste già nella destinazione.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di schemi di partizione da trasferire: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|Lo schema "%1" non esiste nell'origine.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Lo schema "%1" esiste già nella destinazione.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di schemi da trasferire: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|L'assembly SQL "%1" non esiste nell'origine.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|L'assembly SQL "%1" esiste già nella destinazione.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di assembly SQL da trasferire: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|La funzione di aggregazione definita dall'utente "%1" non esiste nell'origine.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|La funzione di aggregazione definita dall'utente "%1" esiste già nella destinazione.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di funzioni di aggregazione definite dall'utente da trasferire: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|Il tipo definito dall'utente (UDT) "%1" non esiste nell'origine.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|Il tipo definito dall'utente (UDT) "%1" esiste già nella destinazione.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di tipi definiti dall'utente (UDT) da trasferire: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|La raccolta di schemi XML "%1" non esiste nell'origine.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|La raccolta di schemi XML "%1" esiste già nella destinazione.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di raccolte di schemi XML da trasferire: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Il trasferimento degli oggetti di tipo "%1" è supportato solo tra computer in cui è in esecuzione SQL Server 2005 o versioni più recenti.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|L'elenco dei database è vuoto.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|L'account di accesso "%1" non esiste nell'origine.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|L'account di accesso "%1" esiste già nella destinazione.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di account di accesso da trasferire: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|L'utente "%1" non esiste nell'origine.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|L'utente "%1" esiste già nella destinazione.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|Si è verificato un errore durante il tentativo di recupero/impostazione dell'elenco di utenti da trasferire: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|L'attività non può includere una gestione connessione mantenuta in una transazione.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|Impossibile ottenere dati XML in formato Unicode da SQL Server perché il provider non supporta la proprietà OUTPUTENCODING.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|Impossibile trovare la gestione connessione FILE "%2" per l'operazione FTP "%1".|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|Gli "account di accesso" sono oggetti a livello server e non possono essere eliminati poiché il server di origine e di destinazione è lo stesso. L'eliminazione di oggetti determinerà la rimozione degli account di accesso dall'origine.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|Il parametro "%1" non può essere negativo. Il valore (-1) viene utilizzato come valore predefinito.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Impossibile caricare oggetti Flusso di dati. Verificare che la proprietà Microsoft.SqlServer.PipelineXml.dll sia registrata correttamente.|  
|0xC0204020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Impossibile salvare oggetti Flusso di dati. Verificare che la proprietà Microsoft.SqlServer.PipelineXml.dll sia registrata correttamente.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Impossibile salvare oggetti Flusso di dati.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Impossibile caricare oggetti Flusso di dati|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Impossibile salvare oggetti Flusso di dati. Il formato specificato non è supportato.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Impossibile caricare oggetti Flusso di dati. Il formato specificato non è supportato.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Impossibile impostare la proprietà degli eventi di persistenza XML per gli oggetti Flusso di dati.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Impossibile impostare la proprietà DOM XML di persistenza per gli oggetti Flusso di dati.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Impossibile impostare la proprietà ELEMENT XML di persistenza per gli oggetti Flusso di dati.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Impossibile impostare proprietà di persistenza XML per gli oggetti Flusso di dati.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Impossibile recuperare la raccolta delle proprietà personalizzata per i componenti Flusso di dati.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|Un albero di esecuzione contiene un ciclo.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|L'oggetto %1 "%2" (%3!d!) è disconnesso dal layout.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|ID dell'oggetto layout non valido.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|Un oggetto di input richiesto non è connesso a un oggetto percorso.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|ID di input sincrono %2!d! non valido per %1.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|L'ID di derivazione di %1 è %2!d!, ma dovrebbe essere %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|Il pacchetto contiene due oggetti con il nome duplicato "%1" e "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|"%1" e "%2" sono inclusi nello stesso gruppo di esclusioni, ma non hanno lo stesso input sincrono.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|L'ID di derivazione %1!d! è duplicato per due oggetti nella stessa raccolta. Tali oggetti sono %2 e %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|Impossibile convalidare il layout.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|Impossibile convalidare uno o più componenti.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|Impossibile convalidare il layout e uno o più componenti.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|Errore all'avvio del motore dell'attività Flusso di dati. Impossibile creare uno o più thread necessari.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|Un thread non è riuscito a creare un mutex in fase di inizializzazione.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|Un thread non è riuscito a creare un semaforo in fase di inizializzazione.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|Il sistema segnala un carico di memoria del %1!d! Sono disponibili %2 byte di memoria fisica con %3 byte liberi. Sono disponibili %4 byte di memoria virtuale con %5 byte liberi. Il file di paging contiene %6 byte con %7 byte liberi.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|Errore del buffer durante l'allocazione di %1!d! byte.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|Impossibile creare Gestione buffer.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Le dimensioni del tipo di buffer %1!d! sono di %2!I64d! byte.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|L'elemento %1 è contrassegnato per essere tralasciato (dangling), ma ha un percorso collegato.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|Impossibile completare la convalida di %1. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|Impossibile completare la fase di post-esecuzione per %1. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|Impossibile completare la fase di preparazione per %1. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|Impossibile completare la fase di pre-esecuzione per %1. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|Impossibile completare la fase di pulizia per %1. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|L'ID di derivazione di %1 è %2!d! e non è stato utilizzato in precedenza nell'attività Flusso di dati.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|Impossibile connettere %1 a %2 perché verrebbe creato un ciclo.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|Impossibile confrontare il tipo di dati "%1". Il confronto di tale tipo di dati non è supportato, pertanto non è possibile utilizzarlo per l'ordinamento o come chiave.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|Questo thread è chiuso non accetta buffer in input.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS codice di errore DTS_E_THREADFAILED.  Chiusura del thread "%1" con codice di errore 0x%2!8.8X!.  Possono essere presenti ulteriori messaggi di errore prima di questo con informazioni aggiuntive sui motivi della chiusura del thread.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS codice di errore DTS_E_PROCESSINPUTFAILED.  Esecuzione del metodo ProcessInput sul componente "%1" (%2!d!) durante l'elaborazione dell'input "%4" (%5!d!) non riuscita. Codice di errore: 0x%3!8.8X! Il componente specificato ha restituito un errore dal metodo ProcessInput. L'errore è specifico del componente ma è irreversibile e causerà l'arresto dell'esecuzione dell'attività Flusso di dati.  Possono essere presenti ulteriori messaggi di errore prima di questo con informazioni aggiuntive sull'errore.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|Impossibile realizzare un set di buffer virtuali.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|Il numero di thread richiesti per la pipeline è %1!d!, ovvero superiore al limite di sistema di %2!d!. La pipeline richiede la configurazione di un numero di thread troppo elevato. Sono presenti troppi output asincroni oppure il valore impostato per la proprietà EngineThreads è troppo alto. Suddividere la pipeline in più pacchetti oppure ridurre il valore della proprietà EngineThreads.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|L'utilità di pianificazione del motore flusso di dati non è in grado di ottenere il conteggio delle origini nel layout.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|L'utilità di pianificazione del motore flusso di dati non è in grado di ottenere il conteggio delle destinazioni nel layout.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|Vista del componente non disponibile. Verificare che la vista del componente sia stata creata.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|L'ID della vista del componente non è corretto. È possibile che la vista del componente non sia sincronizzata. Provare a rilasciare la vista del componente e ricrearla.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|Il buffer non è bloccato. Impossibile manipolarlo.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|L'attività Flusso di dati non è in grado di allocare memoria per la compilazione di una definizione di buffer. La definizione di buffer include %1!d! colonne.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|L'attività Flusso di dati non è in grado di registrare un tipo di buffer. Il tipo include %1!d! colonne ed è destinato all'albero di esecuzione %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|Impossibile modificare la proprietà UsesDispositions rispetto al valore iniziale. Questo errore si verifica in caso di modifica del codice XML e del valore UsesDispositions. Questo valore viene impostato dal componente al momento dell'aggiunta al pacchetto e non è consentita la modifica|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|L'attività Flusso di dati non è riuscita a inizializzare un thread richiesto. Impossibile avviare l'esecuzione. Il thread ha segnalato in precedenza un errore specifico.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|L'attività Flusso di dati non è riuscita a creare un thread richiesto. Impossibile avviare l'esecuzione. Questo errore si verifica in genere a causa di una condizione di memoria insufficiente.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|Impossibile impostare l'input sincrono di "%1" su "%2" perché verrebbe creato un ciclo.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|La proprietà personalizzata denominata "%1" non è valida perché esiste una proprietà predefinita con tale nome. Impossibile utilizzare il nome di una proprietà predefinita per una proprietà personalizzata nello stesso oggetto.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|Buffer già sbloccato.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|Impossibile inizializzare %1. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|Errore di %1 durante la chiusura. Codice di errore restituito: 0x%2!8.8X!. Un componente non è riuscito a rilasciare le interfacce in uso.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS codice di errore DTS_E_PRIMEOUTPUTFAILED.  Il metodo PrimeOutput su %1 ha restituito il codice di errore 0x%2!8.8X!.  Il componente ha restituito un codice di errore quando il motore della pipeline ha chiamato il metodo PrimeOutput (). Il significato del codice di errore è definito dal componente, ma l'errore è irreversibile e ha causato l'arresto dell'esecuzione della pipeline.  Possono essere presenti ulteriori messaggi di errore prima di questo con informazioni aggiuntive sull'errore.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS codice di errore DTS_E_THREADCANCELLED.  Il thread "%1" ha ricevuto un segnale di chiusura e verrà terminato. La chiusura è stata richiesta dall'utente oppure la causa della richiesta di chiusura della pipeline è un errore in un altro thread.  Possono essere presenti ulteriori messaggi di errore prima di questo con informazioni aggiuntive sui motivi dell'annullamento del thread.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|Il distributore del thread "%1" non è riuscito a inizializzare la proprietà "%2" nel componente "%3" a causa dell'errore 0x%8.8X. Impossibile inizializzare la proprietà del componente e impossibile continuare l'esecuzione.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|L'attività Flusso di dati non è in grado di registrare un tipo di buffer di visualizzazione. Il tipo include %1!d! colonne ed è destinato all'ID di input %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|Memoria insufficiente per creare un albero di esecuzione.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|Memoria insufficiente per inserire un oggetto nella tabella hash.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|L'oggetto non è contenuto nella tabella hash.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Impossibile creare una vista del componente perché ne esiste già una. È consentita una sola vista del componente alla volta.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|Nell'input "%1" (%2!d!) la raccolta delle colonne di input virtuali non contiene una colonna di input virtuale con ID di derivazione %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|Il tipo dell'oggetto richiesto non è corretto.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|Gestione buffer non è in grado di creare un file di archiviazione temporanea in nessun percorso specificato nella proprietà BufferTempStoragePath. Nome di file non corretto o autorizzazioni insufficienti o percorsi pieni.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|Gestione buffer non è in grado di eseguire la ricerca fino all'offset %1!d! nel file "%2". Il file è danneggiato.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|Gestione buffer non è in grado di estendere il file "%1" fino alla lunghezza %2!lu! byte.  Spazio su disco insufficiente.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|Gestione buffer non è in grado di scrivere %1!d! byte nel file "%2". Spazio su disco o quote insufficienti.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|Gestione buffer non è in grado di leggere %1!d! byte dal file "%2". Il file è danneggiato.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|L'ID buffer %1!d! supporta altri buffer virtuali e non è possibile attivare la modalità sequenziale. Chiamata di IDTSBuffer100.SetSequentialMode su un buffer che supporta buffer virtuali.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|Impossibile eseguire l'operazione perché il buffer è in modalità sola lettura. I buffer in modalità sola lettura non possono essere modificati.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|Impossibile impostare l'ID %1 su %2!d! poiché verrebbe creato un ciclo.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|Memoria insufficiente per Gestione buffer durante il tentativo di estensione della tabella dei tipi di buffer. a causa di una condizione di memoria insufficiente.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|Gestione buffer non è riuscito a creare un nuovo tipo di buffer.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|L'utilità di pianificazione del motore flusso di dati non è riuscita a recuperare l'albero di esecuzione con indice %1!d! dal layout. Il conteggio ricevuto contiene più alberi di esecuzione di quelli effettivamente esistenti.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|L'attività Flusso di dati non è riuscita a creare un buffer per chiamare PrimeOutput per l'output "%3" (%4!d!) sul componente "%1" (%2!d!). Questo errore è in genere causato da una condizione di memoria insufficiente.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|L'utilità di pianificazione del motore flusso di dati non è riuscita a creare un oggetto thread a causa di una condizione di memoria insufficiente.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|L'utilità di pianificazione del motore flusso di dati non è in grado di recuperare l'oggetto con ID %1!d! dal layout. L'utilità di pianificazione del motore flusso di dati ha individuato in precedenza un oggetto che non è più disponibile.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|L'attività Flusso di dati non è riuscita a preparare i buffer per il nodo dell'albero di esecuzione a partire dall'output "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|L'attività Flusso di dati non è in grado di creare un buffer virtuale per i preparativi per l'esecuzione.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|Raggiunto il limite massimo di ID. Non sono disponibili ulteriori ID da assegnare agli oggetti.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|%1 è già allegato e non può essere collegato di nuovo.  Scollegarlo e riprovare.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|Impossibile utilizzare il nome di colonna "%1" nell'output "%2". È in conflitto con una colonna avente lo stesso nome nell'input sincrono "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|L'attività Flusso di dati non è in grado di creare un buffer per contrassegnare la fine del set di righe.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|Un componente utente gestito ha generato l'eccezione "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|L'utilità di pianificazione del motore flusso di dati non è in grado di allocare memoria sufficiente per le strutture di esecuzione. Memoria insufficiente nel sistema prima dell'avvio dell'esecuzione.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|Impossibile creare l'oggetto buffer a causa di una condizione di memoria insufficiente.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|Impossibile eseguire il mapping degli ID di derivazione di un buffer con gli indici di DTP_HCOL a causa di una condizione di memoria insufficiente.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!" non è in grado di memorizzare la raccolta Variables nella cache. Codice di errore restituito: 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1" non è in grado di memorizzare l'oggetto metadati del componente nella cache. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|La proprietà SortKeyPosition di "%1" è impostata su un valore diverso da zero, ma il valore (%2!ld!) è troppo grande. Deve essere minore o uguale al numero di colonne.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|La proprietà IsSorted di %1 è impostata su TRUE, ma i valori assoluti delle proprietà SortKeyPositions per le colonne di output diverse da zero non compongono una sequenza a incremento progressivo costante a partire da uno.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|Convalida non riuscita per "%1". Stato di convalida restituito: "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|Impossibile creare il componente "%1". Codice di errore restituito: 0x%2!8.8X! "%3!s!". Verificare che il componente sia registrato in modo corretto.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|Il modulo contenente "%1" non è registrato o installato correttamente.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|Impossibile individuare il modulo contenente "%1" anche se è registrato.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|Il componente di script è configurato per la precompilazione dello script, ma non è possibile trovare il codice binario. Fare clic sul pulsante Progetta script per accedere all'IDE nell'editor del componente di script in modo che il codice binario venga generato automaticamente.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|Gestione buffer non è in grado di creare un file per lo spooling di un oggetto long nelle directory specificate nella proprietà BLOBTempStoragePath.  Il nome di file specificato non è corretto, non sono disponibili le autorizzazioni necessarie o i percorsi sono pieni.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|Il valore della proprietà SynchronousInputID in "%1" è %2!d!. Il valore previsto è %3!d!.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|Nessun oggetto esistente con ID %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Impossibile individuare un oggetto con ID %1!d!. Codice di errore: 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|La tabella codici %1!d! specificata nella colonna di output "%2" (%3!d!) non è valida. Selezionare una diversa tabella codici per la colonna di output "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|"%1" non è in grado di memorizzare la raccolta EventInfos nella cache. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|Il nome per "%1" è duplicato.  Tutti i nomi devono essere univoci.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|Nessuna colonna di output associata alla colonna di input "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" dispone di un buffer virtuale esteso da un'origine radice. Esiste un gruppo di esclusioni diverso da zero con un input sincrono zero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" non può essere un output degli errori perché non è possibile posizionare gli output degli errori in output sincroni non esclusivi.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|Si è verificato un errore di divisione per zero. L'operando di destra restituisce zero nell'espressione "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|Il valore letterale "%1" è troppo grande per il tipo %2. La grandezza del valore letterale causa un overflow del tipo.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|Il risultato dell'operazione binaria "%1" sui tipi di dati %2 e %3 supera le dimensioni massime consentite per i tipi numerici. Non è possibile eseguire il cast implicito dei tipi degli operandi a un risultato numerico (DT_NUMERIC) senza perdita di precisione o scala. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|Il risultato dell'operazione binaria "%1" supera le dimensioni massime previste per il tipo di dati del risultato "%2". La grandezza del risultato dell'operazione causa l'overflow del tipo del risultato.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|Il risultato della chiamata di funzione "%1" è troppo grande per il tipo "%2". La grandezza del risultato della chiamata di funzione causa un overflow del tipo dell'operando. Potrebbe essere necessario un cast esplicito a un tipo di grandezza maggiore.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|I tipi di dati "%1" e "%2" non sono compatibili per l'operatore binario "%3". Non è possibile eseguire il cast implicito dei tipi degli operandi in tipi compatibili per l'operazione. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|Impossibile utilizzare il tipo di dati "%1" con l'operatore binario "%2". Il tipo di uno o entrambi gli operandi non è supportato per l'operazione. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|Non corrispondenza di segno per l'operatore binario bit per bit "%1" nell'operazione "%2". Entrambi gli operandi per l'operatore devono essere positivi o negativi.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|Impossibile eseguire l'operazione binaria "%1". Codice di errore: 0x%2!8.8X!. Si è verificato un errore interno o esiste una condizione di memoria insufficiente.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Tentativo di impostazione del tipo di risultato dell'operazione binaria "%1" non riuscito con codice di errore 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Impossibile confrontare "%1" con la stringa "%2".|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|Impossibile utilizzare il tipo di dati "%1" con l'operatore unario "%2". Il tipo di operando non è supportato per l'operazione. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|Impossibile eseguire l'operazione unaria "%1". Codice di errore: 0x%2!8.8X!. Si è verificato un errore interno o esiste una condizione di memoria insufficiente.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Tentativo di impostazione del tipo di risultato dell'operazione unaria "%1" non riuscito con codice di errore 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|La funzione "%1" non supporta il tipo di dati "%2" per il parametro numero %3!d!. Impossibile eseguire il cast implicito del tipo del parametro in un tipo compatibile per la funzione. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|Impossibile riconoscere la funzione "%1". Il nome della funzione non è corretto o non esiste.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|La lunghezza %1!d! non è valido per la funzione "%2". Il parametro della lunghezza non può essere negativo. Modificare il parametro della lunghezza impostando il valore zero o un valore positivo.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|Indice iniziale % 1! d! non è valido per la funzione "%2". Il valore di indice iniziale deve essere un numero intero maggiore di 0. L'indice iniziale è in base 1 e non in base 0.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|La funzione "%1" non è in grado di eseguire il mapping dei caratteri nella stringa "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" non è una parte della data valida per la funzione "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Il parametro numero %1!d! della funzione NULL con tipo di dati "%2" non è valido. I parametri della funzione NULL () devono essere statici e non possono contenere elementi dinamici come le colonne di input.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Il parametro numero %1!d! della funzione NULL con tipo di dati "%2" non è un Integer. I parametri della funzione NULL() devono essere numeri interi o valori di un tipo convertibile in numero intero.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Il parametro numero %1!d! della funzione "%2" non è statico. Il parametro deve essere statico e non può contenere elementi dinamici come le colonne di input.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Il parametro numero %1!d! del cast al tipo di dati "%2" non è valido. I parametri degli operatori cast devono essere statici e non possono contenere elementi dinamici come le colonne di input.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Il parametro numero %1!d! del cast al tipo di dati "%2" non è un Integer. I parametri degli operatori cast devono essere numeri interi o valori di un tipo convertibile in numero intero.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Impossibile eseguire il cast dell'espressione "%1" dal tipo di dati "%2" al tipo di dati "%3". Il cast richiesto non è supportato.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Tentativo di analisi dell'espressione "%1" non riuscito.  Token "%2" non riconosciuto alla riga numero "%3", numero di carattere "%4". Impossibile analizzare l'espressione perché contiene elementi non validi nella posizione specificata.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|Errore durante l'analisi dell'espressione "%1" per cause sconosciute.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Tentativo di analisi dell'espressione "%1" non riuscito. Codice di errore restituito: 0x%2!8.8X!. Impossibile analizzare l'espressione. È possibile che contenga elementi non validi o che il formato non sia corretto. La causa potrebbe anche essere un errore di memoria insufficiente.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|L'espressione "%1" non è valida. Impossibile analizzarla. È possibile che l'espressione contenga elementi non validi o che il formato non sia corretto.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|Nessuna espressione da calcolare. Tentativo di calcolare o recuperare la stringa di un'espressione vuota.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Tentativo di calcolo dell'espressione "%1" non riuscito con codice di errore 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Tentativo di generazione di una rappresentazione stringa dell'espressione non riuscito con codice di errore 0x%1!8.8X!. Errore durante il tentativo di generazione di una stringa visualizzabile che rappresenta l'espressione.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Impossibile convertire il tipo di dati del risultato dell'espressione "%1" nel tipo di dati della colonna "%2". Il risultato dell'espressione dovrebbe essere scritto in una colonna di input/output, ma non è possibile convertire il tipo di dati dell'espressione nel tipo di dati della colonna.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|Tipo di dati "%2" non valido nell'espressione condizionale "%1" dell'operatore condizionale. L'espressione condizionale dell'operatore condizionale deve restituire un valore booleano di tipo DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|I tipi di dati "%1" e "%2" non sono compatibili per l'operatore condizionale. Impossibile eseguire il cast implicito dei tipi degli operandi in tipi compatibili per l'operazione condizionale. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Tentativo di impostazione del tipo di risultato dell'operazione condizionale "%1" non riuscito con codice di errore 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|Buffer orfano. Gestione buffer è stato chiuso lasciando un buffer in sospeso e non verrà eseguita alcuna operazione di pulizia. Potrebbero verificarsi perdite di memoria o altri problemi.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Tentativo di individuazione della colonna di input denominata "%1" non riuscito con codice di errore 0x%2!8.8X!. Impossibile trovare la colonna di input specificata nella raccolta delle colonne di input.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Tentativo di individuazione della colonna di input con ID %1!d! non riuscito con codice di errore 0x%2!8.8X!. Impossibile trovare la colonna di input nella raccolta delle colonne di input.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|Token non riconosciuto "%1" nell'espressione. Se "%1" è una variabile, deve essere espressa nel formato "\@%1". Il token specificato non è valido. Se il token viene usato come nome di variabile, dovrebbe essere preceduto dal simbolo \@.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|Token non riconosciuto "#%1!d!" nell'espressione.|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|Impossibile trovare la variabile "%1" nella raccolta Variables. È possibile che la variabile non esista nell'ambito corretto.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Tentativo di analisi dell'espressione "%1" non riuscito. È possibile che l'espressione contenga un token non valido, un token incompleto o un elemento non valido. È inoltre possibile che il formato dell'espressione non sia corretto o che nell'espressione manchi una parte di un elemento obbligatorio, come una parentesi.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|Il nome di "%1" è vuoto e i nomi non possono essere vuoti.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|La proprietà HasSideEffects di "%1" è impostata su TRUE, ma l'input "%1" è sincrono e pertanto non può avere effetti collaterali. Impostare la proprietà HasSideEffects su FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|Valore %1!d! non valido specificato per il parametro della tabella codici del cast al tipo di dati "%2". La tabella codici non è installata nel computer.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|Il valore %1!d! specificato per il parametro della precisione del cast al tipo di dati "%2" non è valido. La precisione deve essere un valore compreso nell'intervallo da %3!d! a %4!d! e il valore della precisione non è compreso nell'intervallo valido per il cast del tipo.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|Il valore %1!d! specificato per il parametro della scala del cast al tipo di dati "%2" non è valido. La scala deve essere un valore compreso nell'intervallo da %3!d! a %4!d! e il valore di scala non è compreso nell'intervallo valido per il cast del tipo. La scala non deve essere maggiore della precisione e deve essere un valore positivo.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|La proprietà IsSorted di "%1" è impostata su false, ma %2!lu! delle proprietà SortKeyPositions delle colonne di output sono diverse da zero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|Le tabelle codici devono corrispondere per gli operandi dell'operazione condizionale "%1" per il tipo %2. La tabella codici dell'operando di sinistra non corrisponde alla tabella codici dell'operando di destra. Per l'operatore condizionale sul tipo specificato, le tabelle codici devono essere uguali.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|L'input "%1" (%2!d!) fa riferimento all'input "%3" (%4!d!), ma non è presente lo stesso numero di colonne. L'input %5!d! include %6!d! colonne, mentre l'input %7!d! include %8!d! colonne.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|Nessun oggetto esistente con ID di derivazione %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|Impossibile trovare la colonna di output per il nome di file.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|La colonna di output per il nome di file non è una stringa di caratteri Unicode con terminazione Null, corrispondente al tipo di dati DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|Un distributore non è riuscito ad assegnare un buffer al thread "%1" a causa dell'errore 0x%2!8.8X!. Il thread di destinazione è probabilmente in fase di chiusura.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|LocaleID %1!ld! non installato nel sistema.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|Il valore letterale stringa "%1" contiene la sequenza di escape esadecimale "\x%2" non valida. La sequenza di escape non è supportata nei valori letterali stringa nell'analizzatore di espressioni. Le sequenze di escape esadecimali devono essere nel formato \xhhhh dove h è una cifra esadecimale valida.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|Il valore letterale stringa "%1" contiene la sequenza di escape "\\%2!c!" non valida. La sequenza di escape non è supportata nei valori letterali stringa nell'analizzatore di espressioni. Se è necessario inserire una barra rovesciata nella stringa, usare una doppia barra rovesciata, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" non contiene colonne di output. Un output asincrono deve contenere colonne di output.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|A "%1" è assegnato un tipo di dati oggetto long DT_TEXT, DT_NTEXT o DT_IMAGE, non supportato.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Errore dell'output con ID %1!d! sono state assegnate più configurazioni di output degli errori. Prima %2!d! e %3!d!, poi %4!d! e %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|Errore del provider OLE DB durante la verifica della conversione del tipo di dati per "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|Il buffer rappresenta la fine del set di righe e il conteggio delle righe non può essere modificato.  Tentativo di chiamare AddRow o RemoveRow su un buffer con il flag di fine del set di righe.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|Il tipo di dati "%1" non è supportato in un'espressione. Il tipo specificato non è supportato o non è valido.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|L'esecuzione del metodo PrimeOutput su "%1" è stata completata con esito positivo, ma non è stata segnalata la fine del set di righe. Errore nel componente che avrebbe dovuto segnalare una fine di riga. La pipeline interromperà l'esecuzione per evitare risultati imprevisti.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|Overflow durante la conversione dal tipo di dati "%1" al tipo di dati "%2". Il tipo di origine è troppo grande per il tipo di destinazione.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|La conversione dal tipo di dati "%1" al tipo di dati "%2" non è supportata. Impossibile convertire il tipo di origine nel tipo di destinazione.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Codice di errore 0x%1!8.8X! durante il tentativo di conversione dal tipo di dati %2 al tipo di dati %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|Impossibile eseguire l'operazione condizionale "%1". Codice di errore: 0x%2!8.8X!. Si è verificato un errore interno o di memoria insufficiente.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Impossibile eseguire il cast dell'espressione "%1" dal tipo di dati "%2" al tipo di dati "%3". Codice di errore: 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Impossibile valutare la funzione "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Il parametro numero %1!d! della funzione "%2" non può essere convertito in un valore statico.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|Impossibile impostare la disposizione per le righe con errori in "%1" sul reindirizzamento delle righe quando è abilitata l'opzione di caricamento rapido e le dimensioni massime dei commit di inserimento sono impostate su zero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|Le tabelle codici degli operandi dell'operatore binario "%1" per il tipo "%2", devono corrispondere. Attualmente la tabella codici dell'operando sinistro non corrisponde alla tabella codici dell'operando destro. Per l'operatore binario specificato sul tipo specificato le tabelle codici devono essere uguali.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Impossibile recuperare il valore della variabile "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|Tipo di dati della variabile "%1" non supportato in un'espressione.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Impossibile eseguire il cast dell'espressione "%1" dal tipo di dati "%2" al tipo di dati "%3". La tabella codici del valore sottoposto a cast (%4!d!) non corrisponde alla tabella codici (%5!d!) richiesta per il risultato. La tabella codici dell'origine deve corrispondere alla tabella codici richiesta per la destinazione.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|Le dimensioni del buffer predefinito devono essere comprese tra %1!d! e %2!d! byte. È stato eseguito un tentativo di impostazione della proprietà DefaultBufferSize su un valore troppo piccolo o troppo grande.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|Il numero massimo di righe del buffer predefinito deve essere maggiore di %1!d! righe. È stato eseguito un tentativo di impostazione della proprietà DefaultBufferMaxRows su un valore troppo piccolo.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|La tabella codici in %1 è %2!d! e deve essere %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Impossibile assegnare% 3! d! alla proprietà EngineThreads dell'attività Flusso di dati. Il valore deve essere compreso tra %1!d! e %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Analisi dell'espressione "%1" non riuscita. È presente una virgoletta singola imprevista in corrispondenza del numero di riga "%2", numero di carattere "%3".|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Analisi dell'espressione "%1" non riuscita. È presente un segno di uguale (=) imprevisto in corrispondenza del numero di riga "%2", numero di carattere "%3". Nella posizione specificata potrebbe essere richiesto un segno di uguale doppio (==).|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|Il componente "%1" non è riuscito a memorizzare nella cache la raccolta di registrazione dei riferimenti agli oggetti di run-time. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|Esistono più colonne di input con il nome "%1". È necessario specificare la colonna di input desiderata qualificandola in modo univoco come [Nome componente].[%2] oppure è possibile farvi riferimento con l'ID di derivazione. Attualmente, la colonna di input specificata esiste in più di un componente.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Impossibile individuare la colonna di input denominata "[%1].[%2]". Codice di errore: 0x%3!8.8X!. Impossibile trovare la colonna di input nella raccolta delle colonne di input.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|Esistono più variabili con il nome "%1". È necessario specificare la variabile desiderata qualificandola in modo univoco come \@[Spazio dei nomi::%2]. La variabile esiste in più di uno spazio dei nomi.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|L'utilità di pianificazione del motore flusso di dati non è riuscita a ridurre il piano di esecuzione per la pipeline. Impostare la proprietà OptimizedMode su false.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|Impossibile applicare la funzione SQRT a valori negativi. È stato passato un valore negativo alla funzione SQRT.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|Impossibile applicare la funzione LN a valori negativi o pari a zero. È stato passato un valore zero o negativo alla funzione LN.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|Impossibile applicare la funzione LOG a valori negativi o pari a zero. È stato passato un valore zero o negativo alla funzione LOG.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|Impossibile valutare i parametri passati alla funzione POWER. La funzione ha restituito un risultato indeterminato.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|Il runtime non è in grado di fornire un evento di annullamento a causa dell'errore 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|Richiesta di annullamento ricevuta dalla pipeline. La pipeline verrà chiusa.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|Il risultato dell'operazione con operatore meno unario (negazione) "%1" supera le dimensioni massime consentite per il tipo di dati del risultato "%2". La grandezza del risultato dell'operazione causa l'overflow del tipo del risultato.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|Un'espressione contiene il segnaposto "%1". È necessario sostituirlo con un parametro o un operando effettivo.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|La lunghezza %1!d! specificata per la funzione "%2" è negativa e non è valida. Il parametro della lunghezza deve essere positivo.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|Il conteggio delle ripetizioni %1!d! è negativo e non è valido per la funzione "%2". Il parametro per il conteggio delle ripetizioni non può essere negativo.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Impossibile leggere la variabile "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|Per gli operandi di un'operazione binaria, il tipo di dati DT_STR è supportato solo per le colonne di input e le operazioni cast. L'espressione "%1" include un operando DT_STR che non è una colonna di input o il risultato di un cast e che pertanto non può essere utilizzato in un'operazione binaria. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|Per gli operandi dell'operatore condizionale, il tipo di dati DT_STR è supportato solo per le colonne di input e le operazioni cast. L'espressione "%1" include un operando DT_STR che non è una colonna di input o il risultato di un cast e che pertanto non può essere utilizzato in un'operazione condizionale. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|Il conteggio delle occorrenze %1!d! non è valido per la funzione "%2". Il valore del parametro deve essere maggiore di zero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" non è riuscito a memorizzare la raccolta LogEntryInfos nella cache. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|Il parametro della parte della data specificato per la funzione "%1" non è valido. Deve essere una stringa statica.  Il parametro della parte della data non può contenere elementi dinamici, come le colonne di input, e deve essere di tipo DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|Il valore %1!d! specificato per il parametro della lunghezza del cast al tipo di dati %2 è negativo e non è valido. La lunghezza deve essere un valore positivo.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|Il valore %1!d! non valido specificato per il parametro della tabella codici della funzione NULL con tipo di dati "%2". La tabella codici non è installata nel computer.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|Il valore %1!d! specificato per il parametro della precisione della funzione NULL con tipo di dati "%2" non è compreso nell'intervallo valido. La precisione deve essere un valore compreso nell'intervallo da %3!d! a %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|Il valore %1!d! specificato per il parametro della scala della funzione NULL con tipo di dati %2 non è compreso nell'intervallo valido. La scala deve essere compresa nell'intervallo da %3!d! a %4!d!. Il valore della scala non deve essere superiore a quello della precisione e non può essere negativo.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|Il valore %1!d! specificato per il parametro della lunghezza della funzione "NULL" con tipo di dati %2 è negativo e non è valido. La lunghezza deve essere un valore positivo.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|Impossibile assegnare un valore negativo a %1.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|Impossibile impostare la proprietà personalizzata "%1" per "%2" su true.  Il tipo di dati di colonna deve essere uno dei seguenti:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2 o DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|Impossibile ricollegare "%1". Eliminare il percorso, aggiungerne uno nuovo e quindi collegarlo.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|La funzione "%1" richiede %2!d! parametri e non %3!d! parametri. Il nome della funzione è stato riconosciuto ma il numero di parametri non è valido.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|La funzione "%1" richiede %2!d! parametro e non %3!d! parametri. Il nome della funzione è stato riconosciuto ma il numero di parametri non è valido.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|La funzione "%1" richiede %2!d! parametri e non %3!d! parametri. Il nome della funzione è stato riconosciuto ma il numero di parametri non è valido.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Tentativo di analisi dell'espressione "%1" non riuscito a causa di un errore di memoria insufficiente.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 non è riuscito a eseguire il controllo richiesto del livello di prodotto. Codice di errore restituito: 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS codice di errore DTS_E_PRODUCTLEVELTOLOW.  Impossibile eseguire %1 sull'edizione installata %2 di Integration Services. È necessario utilizzare %3 o una versione successiva.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|Un valore letterale stringa nell'espressione supera la lunghezza massima consentita di %1!d! caratteri.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|La variabile %1 contiene una stringa che supera la lunghezza massima consentita di %2!d! caratteri.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|È stato trovato %1 ma non supporta un' interfaccia di Integration Services necessaria (IDTSRuntimeComponent100).  Richiedere una versione aggiornata del componente al provider di componenti.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|Impossibile aprire la chiave del Registro di sistema "%1".|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Impossibile recuperare il nome di file per il componente con CLSID "%1". Verificare che il componente sia registrato correttamente o che il CLSID specificato sia corretto.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|Il CLSID di uno dei componenti non è valido. Verificare che a tutti i componenti nella pipeline sia associato un CLSID valido.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|Il CLSID di uno dei componenti con ID %1!d! non è valida.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|Indice non valido.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|Impossibile accedere all'oggetto Application. Verificare che SSIS sia installato correttamente.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Impossibile recuperare il nome di file di un componente. Codice di errore: 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Impossibile recuperare la proprietà "%1" dal componente con ID %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Tentativo di utilizzare l'ID %1!d! più di una volta nell'attività Flusso di dati.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Impossibile recuperare un elemento in base all'ID di derivazione da una raccolta che non contiene colonne.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Impossibile trovare la gestione connessione con ID "%1" nella raccolta delle gestioni connessioni. Codice di errore: 0x%2!8.8X!. La gestione connessione è richiesta da "%3" nella raccolta delle gestioni connessioni di "%4". Verificare che nella raccolta delle gestioni connessioni Connections sia stata creata una gestione connessione con tale ID.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|Il thread "%1" ha ricevuto un buffer per l'input %2!d!, ma il thread non è responsabile di tale input. Si è verificato un errore, a causa del quale l'utilità di pianificazione del motore flusso di dati ha compilato un piano di esecuzione non valido.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|Il componente "%1" (%2!d!) non è in grado di fornire un'interfaccia IDTSRuntimeComponent100.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|Il motore dell'attività Flusso di dati ha tentato di copiare un buffer per assegnare un altro thread, ma il tentativo non è riuscito.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|Il motore dell'attività Flusso di dati non è riuscito a creare un buffer di visualizzazione di tipo %1!d! sul tipo %2!d! per il buffer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|Gestione buffer non ha potuto creare un file temporaneo nel percorso "%1". Il percorso non verrà ripreso in considerazione per l'archiviazione temporanea.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|Il tentativo di Gestione buffer di indirizzare una riga di errore a un output non è stato registrato come output degli errori. Chiamata di DirectErrorRow su un output con proprietà IsErrorOut non impostata su TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|Chiamata a un metodo del buffer su un buffer privato. I buffer privati non supportano questa operazione.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|I buffer in modalità privata non supportano questa operazione.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|Impossibile chiamare l'operazione su un buffer passato a PrimeOutput. È stato chiamato un metodo di un buffer durante PrimeOutput, ma la chiamata non è consentita durante PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|Impossibile chiamare l'operazione su un buffer passato a ProcessInput. È stato chiamato un metodo di un buffer durante ProcessInput, ma la chiamata non è consentita durante ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|Gestione buffer non ha potuto ottenere un nome di file temporaneo.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|Colonna troppo larga nel codice.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Impossibile ottenere l'ID della gestione connessione di run-time specificata da "%1" nella raccolta delle gestioni connessioni Connections di "%2". Codice di errore: 0x%3!8.8X!. Verificare che la proprietà ConnectionManager.ID dell'oggetto connessione di run-time sia impostata per il componente.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|La gestione connessione "%1" nella raccolta delle gestioni connessioni Connections di "%2" non include un valore per la proprietà ID. Verificare che la proprietà ConnectionManagerID dell'oggetto connessione di run-time sia impostata per il componente.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Impossibile modificare i metadati durante l'esecuzione.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|Impossibile aggiornare i metadati del componente per "%1" alla versione più recente del componente. Metodo PerformUpgrade non riuscito.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|La versione di %1 non è compatibile con questa versione di DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|Componente mancante, non registrato, non aggiornabile oppure mancano interfacce necessarie. Informazioni di contatto per il componente: "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|Metodo chiamato sul buffer errato. L'operazione non è supportata dai buffer che non vengono utilizzati per l'output del componente.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|Errore durante il calcolo dell'espressione.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Divisione per zero nell'espressione.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|La grandezza del valore letterale è eccessiva per il tipo richiesto.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|Il risultato di un'operazione binaria è troppo grande per le dimensioni massime previste per i tipi numerici. Non è possibile eseguire il cast implicito dei tipi degli operandi a un risultato numerico (DT_NUMERIC) senza perdita di precisione o scala. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|La grandezza del risultato di un'operazione binaria causa un overflow delle dimensioni massime previste per il tipo di dati del risultato.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|La grandezza del risultato di una chiamata di funzione è troppo grande per il tipo di risultato e ha causato un overflow del tipo dell'operando. Potrebbe essere necessario un cast esplicito a un tipo di grandezza maggiore.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Tipi di dati non compatibili per un operatore binario. Non è possibile eseguire il cast implicito dei tipi degli operandi in tipi compatibili per l'operazione. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|Tipo di dati non supportato per un operatore binario. Il tipo di uno o entrambi gli operandi non è supportato per l'operazione. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|Non corrispondenza di segno per l'operatore binario bit per bit. Gli operandi dell'operatore devono essere entrambi positivi o entrambi negativi.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|Impossibile eseguire un'operazione binaria. Condizione di memoria insufficiente o errore interno.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Impossibile impostare il tipo di risultati di un'operazione binaria.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Impossibile confrontare due stringhe.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|Tipo di dati non supportato per un operatore unario. Il tipo dell'operando non è supportato per l'operazione. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|Impossibile eseguire un'operazione unaria. Condizione di memoria insufficiente o errore interno.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Impossibile impostare il tipo di risultati di un'operazione unaria.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|Parametro con tipo di dati non supportato in una funzione. Impossibile eseguire il cast implicito del tipo di parametro in un tipo compatibile per la funzione. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|Nome di funzione non valido nell'espressione. Verificare che il nome della funzione sia corretto ed esista.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|Parametro della lunghezza non valido per la funzione SUBSTRING. Il parametro della lunghezza non può essere negativo.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|Indice iniziale non valido per la funzione SUBSTRING. Il valore di indice iniziale deve essere un numero intero maggiore di zero. L'indice iniziale è in base 1 e non in base 0.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|Il numero di parametri passati a una funzione non è valido. Il nome della funzione è stato riconosciuto, ma il numero di parametri non è corretto.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|Impossibile eseguire una funzione di mapping dei caratteri.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|Per una funzione di data è stato specificato un parametro della parte della data non riconosciuto.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|Parametro non valido per la funzione NULL. I parametri della funzione NULL devono essere statici e non possono contenere elementi dinamici come le colonne di input.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|Parametro non valido per la funzione NULL. I parametri della funzione NULL devono essere numeri interi o valori di un tipo convertibile in numero intero.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|Parametro non valido per una funzione. Il parametro deve essere statico e non può contenere elementi dinamici come le colonne di input.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|Parametro non valido per un'operazione cast. I parametri degli operatori cast devono essere statici e non possono contenere elementi dinamici come le colonne di input.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|Parametro non valido per un'operazione cast. I parametri degli operatori cast devono essere numeri interi o valori di un tipo convertibile in numero intero.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|Cast di tipo non supportato nell'espressione.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|Token non riconosciuto nell'espressione. Impossibile analizzare l'espressione perché contiene elementi non validi.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|Espressione non valida. Impossibile analizzarla. È possibile che contenga elementi non validi o che il formato non sia corretto.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|Il risultato di un'operazione con un operatore meno unario (negazione) è più grande delle dimensioni massime consentite per il tipo di dati del risultato. La grandezza del risultato dell'operazione causa l'overflow del tipo del risultato.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Tentativo di calcolo dell'espressione non riuscito.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Tentativo di generare una rappresentazione stringa dell'espressione non riuscito.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Impossibile convertire il tipo di dati del risultato dell'espressione nel tipo di dati della colonna. Il risultato dell'espressione dovrebbe essere scritto in una colonna di input/output, ma non è possibile convertire il tipo di dati dell'espressione nel tipo di dati della colonna.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|Tipo di dati non valido per l'espressione condizionale dell'operatore condizionale. Il tipo dell'espressione condizionale deve essere DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|Tipi di dati non compatibili per gli operandi dell'operatore condizionale. Impossibile eseguire il cast implicito dei tipi degli operandi nei tipi compatibili per l'operazione condizionale. Per eseguire questa operazione, è necessario eseguire il cast esplicito di uno o entrambi gli operandi con un operatore cast.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Impossibile impostare il tipo di risultati di un'operazione condizionale.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|Impossibile trovare la colonna di input specificata nella raccolta delle colonne di input.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Impossibile trovare una colonna di input in base all'ID di derivazione. Impossibile trovare la colonna di input nella raccolta delle colonne di input.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|L'espressione contiene un token non riconosciuto che sembra essere un riferimento a una colonna di input, ma la raccolta delle colonne di input non è disponibile per l'elaborazione delle colonne di input. La raccolta delle colonne di input non è stata specificata per l'analizzatore di espressioni, ma l'espressione include una colonna di input.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|Impossibile trovare una variabile specificata nella raccolta. È possibile che non esista nell'ambito corretto. Verificare che la variabile esista e che l'ambito sia corretto.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Tentativo di analisi dell'espressione non riuscito. L'espressione contiene un token non valido o incompleto. È possibile che l'espressione contenga elementi non validi, che manchi una parte di un elemento obbligatorio come una parentesi di chiusura o che il formato non sia corretto.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|Valore non valido specificato per il parametro della tabella codici del cast al tipo di dati DT_STR o DT_TEXT. La tabella codici specificata non è installata nel computer.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|Il valore specificato per il parametro della precisione di un'operazione cast non è compreso nell'intervallo valido per il cast del tipo.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|Il valore specificato per il parametro della scala di un'operazione cast non è compreso nell'intervallo valido per il cast del tipo. Il valore della scala non deve essere superiore a quello della precisione e non può essere negativo.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|Tabelle codici non corrispondenti in un'operazione condizionale. La tabella codici dell'operando di sinistra non corrisponde alla tabella codici dell'operando di destra. Per l'operatore condizionale del tipo specificato, le tabelle codici devono essere uguali.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|Sequenza di escape decimale non valida in un valore letterale stringa. La sequenza di escape non è supportata nei valori letterali stringa nell'analizzatore di espressioni. Le sequenze di escape esadecimali devono essere del formato \xhhhh dove h è una cifra esadecimale valida.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|Sequenza di escape decimale non valida in un valore letterale stringa. La sequenza di escape non è supportata nei valori letterali stringa nell'analizzatore di espressioni. Se è necessario inserire una barra rovesciata nella stringa, usare una doppia barra rovesciata, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|Un tipo di dati non supportato o non riconosciuto nell'espressione.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|Overflow durante la conversione tra tipi di dati. Il tipo di origine è troppo grande per il tipo di destinazione.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|Conversione di tipo di dati non supportata nell'espressione. Impossibile convertire il tipo di origine nel tipo di destinazione.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|Errore durante il tentativo di esecuzione della conversione dei dati. Impossibile convertire il tipo di origine nel tipo di destinazione.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|Impossibile eseguire l'operazione condizionale.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|Errore durante il tentativo di esecuzione di un cast di tipo.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Impossibile convertire "%1" dal tipo DT_STR al tipo DT_WSTR. Codice di errore: 0x%2!8.8X!. Si è verificato un errore durante la conversione implicita nella colonna di input.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Impossibile convertire una colonna di input dal tipo DT_STR al tipo DT_WSTR. Si è verificato un errore durante la conversione implicita nella colonna di input.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|Errore durante la valutazione della funzione.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|Impossibile convertire un parametro della funzione in un valore statico. Il parametro deve essere statico e non può contenere elementi dinamici come le colonne di input.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|Parametro della lunghezza non valido per la funzione RIGHT. Il parametro della lunghezza non può essere negativo.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|Parametro del conteggio delle ripetizioni non valido per la funzione REPLICATE. Il valore del parametro non può essere negativo.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|Tabelle codici non corrispondenti in un'operazione binaria. La tabella codici dell'operando di sinistra non corrisponde alla tabella codici dell'operando di destra. Per questa operazione binaria, le tabelle codici devono essere uguali.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Impossibile recuperare il valore per una variabile.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|L'espressione contiene una variabile con un tipo di dati non supportato.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Impossibile eseguire il cast dell'espressione perché la tabella codici del valore sottoposto a cast non corrisponde alla tabella codici richiesta per il risultato. La tabella codici dell'origine deve corrispondere alla tabella codici richiesta per la destinazione.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|Virgoletta singola imprevista nell'espressione. Potrebbe essere richiesto il segno di virgolette doppie.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|Segno di uguale (=) imprevisto nell'espressione. Questo errore si verifica in genere quando è necessario un segno di uguale doppio (==).|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|Il nome di colonna di input specificato è ambiguo.  Il nome della colonna deve essere qualificato nel formato [Nome componente].[Nome colonna] oppure è necessario fare riferimento alla colonna con l'ID di derivazione. Questo errore si verifica quando la colonna di input esiste in uno o più componenti ed è necessario differenziarlo con l'aggiunta del nome del componente o utilizzando l'ID di derivazione.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|L'espressione contiene un segnaposto per un parametro o un operando della funzione. Il segnaposto deve essere sostituito con il parametro o l'operando effettivo.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|Il nome di variabile specificato è ambiguo. È necessario qualificare la variabile desiderata nel formato \@[Spazio dei nomi::Variabile]. Questo errore si verifica quando la variabile esiste in più di uno spazio dei nomi.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|Per gli operandi di un'operazione binaria, il tipo di dati DT_STR è supportato solo per le colonne di input e le operazioni cast. In un'operazione binaria non è consentito l'utilizzo di un operando DT_STR che non sia una colonna di input o il risultato di un cast. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|Per gli operandi dell'operatore condizionale, il tipo di dati DT_STR è supportato solo per le colonne di input e le operazioni cast. In un'operazione condizionale non è consentito l'utilizzo di un operando DT_STR che non sia una colonna di input o il risultato di un cast. Per eseguire questa operazione, è necessario eseguire il cast esplicito dell'operando con un operatore cast.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|Parametro del conteggio delle occorrenze non valido per la funzione FINDSTRING. Il valore del parametro deve essere maggiore di zero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|Il parametro della parte della data specificato per una funzione di data non è valido. I parametri della parte della data devono essere stringhe statiche e non possono contenere elementi dinamici come le colonne di input. Inoltre, devono essere di tipo DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|Il valore specificato per il parametro della lunghezza di un'operazione cast non è valido. La lunghezza deve essere un valore positivo. La lunghezza specificata per il cast del tipo è negativa. Modificare il valore impostandone uno positivo.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|Il valore specificato per il parametro della lunghezza di una funzione NULL non è valido. La lunghezza deve essere un valore positivo. La lunghezza specificata per la funzione NULL è negativa. Modificare il valore impostandone uno positivo.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|Valore non valido specificato per il parametro della tabella codici della funzione NULL con tipo di dati DT_STR o DT_TEXT. La tabella codici specificata non è installata nel computer. Modificare la tabella codici specificata oppure installare la tabella codici mancante nel computer.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|Il valore specificato per il parametro della precisione di una funzione NULL non è valido. Il valore di precisione specificato non è compreso nell'intervallo valido per la funzione NULL.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|Il valore specificato per il parametro della scala di una funzione NULL non è valido. Il valore di scala specificato non è compreso nell'intervallo valido per la funzione NULL. La scala non deve essere maggiore della precisione e deve essere un valore positivo.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|%1 non è riuscito a scrivere dati in %2 su %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|Richiesta di annullamento dall'utente per la trasformazione Ricerca.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|L'elaborazione dei dati di tipo carattere o BLOB (oggetto binario di grandi dimensioni) è stata arrestata perché è stato raggiunto il limite di 4 GB.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|Impossibile caricare il componente pipeline gestito "%1".  Eccezione: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|Codice di errore SSIS DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: Gestione connessione Excel non è supportato nella versione a 64 bit di SSIS, in quanto non sono disponibili provider OLE DB.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|Il file di cache è danneggiato oppure non è stato creato utilizzando la gestione connessione della cache.  Fornire un file di cache valido.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|Il comando SQL non è impostato in modo corretto. Controllare la proprietà SQLCommand.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|Sono disponibili informazioni sull'oggetto errore COM.  Origine: "%1" Codice di errore: 0x%2!8.8X!  Descrizione: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Impossibile accedere alle connessioni acquisite.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|Il numero di colonne non è corretto.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Impossibile trovare la colonna "%1" nell'origine dei dati.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|È disponibile un record OLE DB.  Origine: "%1" Hresult: 0x%2!8.8X!  Descrizione: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|Codice di errore SSIS DTS_E_OLEDBERROR.  Si è verificato un errore OLE DB. Codice errore: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|Componente già connesso. È necessario disconnettere il componente prima di ritentare la connessione.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|Il valore della proprietà "%1" non è corretto.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Impossibile aprire il file di dati "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|Nessun nome di file flat di destinazione specificato. Verificare che per la gestione connessione file flat sia configurata una stringa di connessione. Se la gestione connessione file flat è utilizzata dai più componenti, verificare che la stringa di connessione includa un numero sufficiente di nomi di file.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|Impossibile trovare il qualificatore di testo per la colonna "%1".|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|La conversione da "%1" a "%2" non è supportata.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|Durante la convalida della conversione del tipo da %2 a %3 è stato restituito il codice di errore 0x%1!8.8X!.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Impossibile trovare la colonna di input con ID di derivazione "%1!d!" richiesta da "%2". Controllare proprietà personalizzata SourceInputColumnLineageID della colonna di output.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|Numero di output non corretto. Devono essere presenti almeno%1!d! output.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|Numero di output non corretto. Il numero esatto di input che devono essere presenti è: %1!d!.|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|Stringa troppo lunga per eseguirne la conversione.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|Numero di input non corretto. Il numero esatto di input che devono essere presenti è: input.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|Il numero di colonne di input per %1 non può essere zero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|Il componente include %1!d! input.  Nessun input consentito per questo componente.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|Chiamata di ProcessInput con l'ID di input non valido %1!d!.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|La proprietà personalizzata "%1" deve essere di tipo %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|Tipo di buffer non valido. Assicurarsi che il layout della pipeline e tutti i componenti superino la convalida.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|Il valore per la proprietà personalizzata "%1" non è corretto.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|Errore dovuto alla mancanza di una connessione. È necessaria una connessione per la richiesta dei metadati. Se è attiva la modalità offline, deselezionare il comando Offline nel menu SSIS per abilitare la connessione.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|Impossibile creare la proprietà personalizzata "%1".|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|Impossibile recuperare la raccolta della proprietà personalizzata per l'inizializzazione.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Impossibile creare una funzione di accesso OLE DB. Verificare che i metadati della colonna siano validi.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|Chiamata di PrimeOutput con l'ID di output non valido %1!d!.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|Il valore per la proprietà "%1" in "%2" non è valido.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|Per leggere i dati è necessaria una connessione.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|Errore durante la lettura delle righe di intestazione.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Nome di colonna duplicato "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Impossibile ottenere il nome della colonna con ID %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Impossibile indirizzare la riga all'output "%1" (%2!d!).|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Impossibile creare il thread per l'inserimento bulk a causa dell'errore "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|Impossibile inizializzare il thread per l'attività Inserimento bulk SSIS.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|Thread per l'attività Inserimento bulk SSIS già in esecuzione.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|Thread per l'attività Inserimento bulk SSIS interrotto con errori o avvisi.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Impossibile aprire un set di righe di caricamento rapido per "%1". Controllare che l'oggetto esista nel database.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Errore dovuto alla mancanza di una connessione. È necessaria una connessione per eseguire la convalida dei metadati.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|Non è stato specificato il nome di una tabella di destinazione.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|Il provider OLE DB utilizzato dall'adattatore OLE DB non supporta IConvertType. Impostare la proprietà ValidateColumnMetaData dell'adattatore su FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|Il provider OLE DB utilizzato dall'adattatore OLE DB non è in grado di eseguire la conversione tra i tipi "%1" e "%2" per "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Convalida dei metadati della colonna non riuscita.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" è una colonna ID di riga e non può essere inclusa in un'operazione di inserimento dati.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Tentativo di inserimento nella colonna della versione di riga "%1". Impossibile eseguire inserimenti in una colonna della versione di riga.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Errore durante l'inserimento nella colonna di sola lettura "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Impossibile recuperare informazioni sulla colonna dall'origine dei dati. Verificare che la tabella di destinazione nel database sia disponibile.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|Impossibile bloccare un buffer. Memoria di sistema insufficiente oppure Gestione buffer ha raggiunto il limite di quote.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|Per %1 è impostata una proprietà ComparisonFlags che include flag aggiuntivi con il valore %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|Metadati della colonna non disponibili per la convalida.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|Impossibile scrivere nel file di dati.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|Impossibile trovare il delimitatore di colonna per la colonna "%1".|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Impossibile analizzare la colonna "%1" nel file di dati.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|Nome di file specificato in modo non corretto.  Specificare il percorso e il nome del file non elaborato direttamente nella proprietà FileName oppure tramite una variabile nella proprietà FileNameVariable.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|Impossibile aprire il file "%1" per la scrittura. Questo errore può verificarsi quando non sono disponibili i privilegi appropriati per il file o il disco è pieno.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|Impossibile creare un buffer di I/O per il file di output. Questo errore può verificarsi quando non sono disponibili i privilegi appropriati per il file o il disco è pieno.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|Impossibile scrivere %1!d! byte nel file "%2". Per ulteriori dettagli, vedere i messaggi di errore precedenti.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Metadati non validi nell'intestazione del file. Il file è danneggiato oppure non è un file di dati non elaborati generato da SSIS.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Si è verificato un errore perché il file di output esiste già e la proprietà WriteOption è impostata per Crea una sola volta. Impostare la proprietà WriteOption su Crea sempre oppure eliminare il file.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Errore causato da impostazioni di proprietà in conflitto. Sia la proprietà AllowAppend che la proprietà ForceTruncate sono impostate su TRUE. Non è consentito impostare entrambe le proprietà su TRUE. Impostare una delle due proprietà su FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|Versione e informazioni sui flag del file non valide. Il file è danneggiato oppure non è un file di dati non elaborati generato da SSIS.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|Il file di output è stato scritto con una versione non compatibile. Impossibile accodarlo. È possibile che il formato del file sia obsoleto e non più utilizzabile.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Impossibile accodare il file di output. Nessuna colonna nel file esistente corrisponde alla colonna "%1" dell'input. Il file esistente non corrisponde nei metadati.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Impossibile accodare il file di output. Il numero di colonne nel file di output non corrisponde al numero di colonne nella destinazione. Il file esistente non corrisponde a livello dei metadati.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|Errore durante il recupero delle informazioni sulla tabella codici della colonna.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Impossibile leggere %1!d! byte dal file "%2". La causa dell'errore dovrebbe essere stata segnalata in precedenza.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Fine del file imprevista durante la lettura di %1!d! byte dal file "%2". Fine prematura del file a causa di un formato di file non valido.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|Impossibile utilizzare la colonna %1. Gli adattatori per dati non elaborati non supportano dati di tipo image, text o ntext.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|Tipo di dati %1!d! non riconosciuto rilevato dall'adattatore. La causa potrebbe essere un file di input danneggiato (origine) o un tipo di buffer non valido (destinazione).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|Stringa troppo lunga. La stringa letta dall'adattatore ha una lunghezza di %1!d! byte, ma è prevista una stringa non più lunga di %2!d! byte, in corrispondenza dell'offset %3!d!. L'errore potrebbe indicare un file di input danneggiato. La lunghezza della stringa nel file è eccessiva per la colonna del buffer.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|L'adattatore per dati non elaborati ha tentato di ignorare %1!d! byte nel file di input per la colonna senza riferimenti "%2" con ID di derivazione %3!d!, ma si è verificato un errore. L'errore restituito dal sistema operativo dovrebbe essere già stato segnalato in precedenza.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|L'adattatore per dati non elaborati ha tentato di leggere %1!d! byte nel file di input per la colonna "%2" con ID di derivazione %3!d!, ma si è verificato un errore. L'errore restituito dal sistema operativo dovrebbe essere già stato segnalato in precedenza.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|Proprietà del nome di file non valida. Il nome di file indica un dispositivo o contiene caratteri non validi.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Impossibile preparare l'attività Inserimento bulk SSIS per l'inserimento dei dati.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|Il nome dell'oggetto di database "%1" non è valido.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Clausola di ordinamento non valida.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|Impossibile aprire il file "%1" per la lettura. Questo errore può verificarsi quando non sono disponibili i privilegi appropriati per il file o è impossibile trovare il file. La causa esatta è indicata nel messaggio di errore precedente.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Impossibile creare Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Impossibile configurare Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Tipo di dati non supportato per la colonna %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|Tentativo di lettura da Microsoft.AnalysisServices.TimeDimGenerator non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|Tentativo di lettura dei dati della colonna "%2!d!" da Microsoft.AnalysisServices.TimeDimGenerator non riuscito. Codice di errore: 0x%2!8.8X!.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|La proprietà VariableName non è impostata sul nome di una variabile valida. È necessario un nome di variabile di run-time in cui scrivere.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Impossibile creare o configurare l'oggetto ADODB.Recordset.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Errore durante la scrittura nell'oggetto ADODB.Recordset.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|Nome file non valido. Il nome di file indica un dispositivo o contiene caratteri non validi.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|Nome di file "%1" non valido. Il nome di file indica un dispositivo o contiene caratteri non validi.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Impossibile recuperare le descrizioni delle colonne di destinazione dai parametri del comando SQL.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Parametri non associati. Tutti i parametri nel comando SQL devono essere associati a colonne di input.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|Il valore PivotUsage per la colonna di input "%1" (%2!d!) non è valido.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Troppe chiavi pivot. È possibile utilizzare una sola colonna di input come chiave pivot.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|Nessuna chiave pivot. È necessario utilizzare una sola colonna di input come chiave pivot.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|Alla colonna di input "%3" (%4!d!) viene eseguito il mapping di più colonne di output (come "%1" (%2!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Impossibile eseguire il mapping della colonna di output "%1" (%2!d!) alla colonna di input PivotKey.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|Il valore SourceColumn %3!d! impostato per la colonna di output "%1" non è un ID di derivazione valido di una colonna di input.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Sulla colonna di output "%1" (%2!d!) viene eseguito il mapping a una colonna di input Valore trasformato tramite Pivot, ma manca il valore della proprietà PivotKeyValue corrispondente.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Sulla colonna di output "%1" (%2!d!) viene eseguito il mapping a una colonna di input Valore trasformato tramite Pivot con un valore non univoco per la proprietà PivotKeyValue.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|Sulla colonna di input "%1" (%2!d!) non viene eseguito il mapping ad alcuna colonna di output.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Errore durante il confronto dei valori per le chiavi del set.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|Impossibile utilizzare la colonna di input "%1" (%2!d!) come Chiave set, Chiave pivot o Valore pivot perché contiene dati di tipo long.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Tipo di output non corretto. Il tipo di dati e i metadati della colonna di output "%1" (%2!d!) devono essere uguali a quelli della colonna di input a cui viene eseguito il mapping."|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Errore durante il tentativo di trasformazione dei record di origine tramite Pivot.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|Il valore della chiave pivot "%1" non è valido.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|Errore durante il tentativo di ignorare le righe di dati.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|Errore durante l'elaborazione del file "%1" nella riga di dati %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|Errore durante l'inizializzazione del parser di file flat.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Impossibile recuperare informazioni sulle colonne dalla gestione connessione file flat.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Impossibile scrivere il nome di colonna per la colonna "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|Il tipo di colonna "%2" per la colonna "%1" non è corretto. Si tratta del tipo "%2". Può essere solo "%3" o "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|Impossibile scrivere %1!d! byte di dati nel buffer di I/O su disco. Nel buffer di I/O su disco sono disponibili %2!d! byte.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|Errore durante la scrittura dell'intestazione del file.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|Errore durante il recupero delle dimensioni del file "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|Errore durante l'impostazione del puntatore per il file "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|Errore durante l'impostazione del buffer di I/O su disco.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|I dati della colonna "%1" causano un overflow del buffer di I/O su disco.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|Errore imprevisto di I/O su disco durante la lettura del file.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|Errore del buffer di I/O su disco durante la lettura del file.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|Impossibile impostare il tipo di utilizzo su lettura/scrittura per le colonne di input di questa trasformazione. Modificare il tipo di utilizzo e impostare sola lettura.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Impossibile copiare o convertire i dati del file flat per la colonna "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Impossibile eseguire la conversione dei dati. La conversione dei dati per la colonna "%1" ha restituito il valore di stato %2!d! e il testo di stato "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|Raccolta Variables non disponibile.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|Valore PivotKeyValue duplicato. Sulla colonna di input "%1" (%2!d!) viene eseguito il mapping a una colonna di output Valore trasformato tramite Pivot e ha un valore non univoco per la proprietà PivotKeyValue.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|Impossibile trovare una destinazione per la trasformazione UnPivot. Su almeno una colonna di input deve essere eseguito il mapping tramite PivotKeyValue a una colonna DestinationColumn nell'output.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|Valore PivotKeyValue non valido. In una trasformazione UnPivot con più di una colonna DestinationColumn trasformata tramite UnPivot, il set di valori PivotKeyValue per ogni destinazione deve corrispondere esattamente.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Metadati UnPivot non corretti. In una trasformazione UnPivot, i metadati di tutte le colonne di input con un valore PivotKeyValue impostato e che puntano alla stessa colonna DestinationColumn devono corrispondere esattamente a DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Impossibile convertire il valore di chiave pivot "%1" nel tipo di dati della colonna chiave pivot.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Troppe chiavi pivot specificate. È possibile utilizzare una sola colonna di output come chiave pivot.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|Sulla colonna di output "%1" (%2!d!) non viene eseguito il mapping a nessuna proprietà DestinationColumn della colonna di input.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|Nessuna colonna di output contrassegnata come PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|Il valore della proprietà DestinationColumn della colonna di input "%1" (%2!d!) non fa riferimento a un valore valido LineageID per una colonna di output.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Errore di destinazione duplicata. Su più di una colonna di input non trasformata tramite Pivot viene eseguito il mapping alla stessa colonna di output di destinazione.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|Impossibile trovare colonne di input. Su almeno una colonna di input deve essere eseguito il mapping a una colonna di output.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|Il numero di colonne di input e di output non è uguale. Il numero totale di colonne di input per tutti gli input deve essere uguale al numero totale di colonne di output.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|Input non ordinato. È necessario ordinare "%1".|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|La proprietà personalizzata JoinType per %1 contiene il valore %2!ld!, non valido. I valori validi sono 0 (full), 1 (left) o 2 (inner).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|Valore NumKeyColumns non valido. In %1, il valore per la proprietà personalizzata NumKeyColumns deve essere compreso nell'intervallo da 1 a %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|Impossibile trovare colonne chiave. È necessario che %1 includa almeno una colonna con un valore SortKeyPosition diverso da zero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Colonne chiave insufficienti. %1 deve includere almeno %2!ld! colonne con valori SortKeyPosition diversi da zero.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Non corrispondenza del tipo di dati. I tipi di dati per le colonne con valore SortKeyPosition %1!ld! non corrispondono.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|La colonna con valore SortKeyPosition %1!ld! non è valida. Il valore dovrebbe essere %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Direzioni di ordinamento non corrispondenti. Le direzioni di ordinamento per le colonne con valore SortKeyPosition %1!ld! non corrispondono.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Colonna mancante. È necessario associare una colonna di input a %1.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Alle colonne di input devono essere associate colonne di output. Sono presenti colonne di input con tipo di utilizzo di sola lettura alle quali non sono associate colonne di output.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|I flag di confronto non sono zero. I flag di confronto per le colonne non stringa devono essere zero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|I flag di confronto per le colonne con valore SortKeyPosition %1!ld! non corrispondono.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Valore di chiave pivot non riconosciuto.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|Il valore dell'elemento di derivazione %1!ld! non è valida. L'intervallo valido è compreso tra %2!ld! e %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Colonne di input non consentite. Il numero di colonne di input deve essere zero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|Il tipo di dati per "%1" non è valido per l'elemento di derivazione specificato.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|La lunghezza per "%1" non è valida per l'elemento di derivazione specificato.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|I metadati per "%1" non corrispondono ai metadati per la colonna di output associata.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|Sono presenti colonne di output con valori SortKeyPosition che non corrispondono al valore SortKeyPosition delle colonne di input associate.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|Tentativo di aggiungere una riga al buffer dell'attività Flusso di dati non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Errore di conversione dei dati durante la conversione dalla colonna "%1" (%2!d!) alla colonna "%3" (%4!d!).  La conversione ha restituito il valore di stato %5!d! e il testo di stato "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|Tentativo di allocazione di un buffer per handle di riga non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|Tentativo di invio di una riga a SQL Server non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|Tentativo di preparazione dello stato del buffer non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|Tentativo di recupero dell'inizio della riga del buffer non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|Thread per l'attività Inserimento bulk SSIS non è più in esecuzione.  Impossibile inserire altre righe. Provare ad aumentare il timeout del thread per l'inserimento bulk.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|File di origine non valido. Il file di origine restituisce un conteggio di più di 131.072 colonne. Questo errore si verifica in genere quando il file di origine non viene generato dalla destinazione dei file non elaborati.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1 è un input aggiuntivo non collegato e verrà rimosso.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|L'elemento %1 non è collegato ma non è contrassegnato per essere tralasciato (dangling).  Verrà contrassegnato per essere tralasciato.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Valore di chiave pivot duplicato "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Valore di chiave pivot duplicato.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Impossibile recuperare l'ID delle impostazioni locali del componente. Codice di errore 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|ID delle impostazioni locali non corrispondenti. L'ID delle impostazioni locali del componente (%1!d!) non corrisponde all'ID delle impostazioni locali della gestione connessione (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|L'ID delle impostazioni locali per il componente non è stato impostato. Per gli adattatori di file flat è necessario impostare l'ID delle impostazioni locali nella gestione connessione file flat.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|Campo binario troppo lungo. Il campo binario letto dall'adattatore ha una lunghezza di %1!d! byte, ma è previsto un campo non più lungo di %2!d! byte in corrispondenza dell'offset %3!d!. Questo errore si verifica in genere quando il file di input non è valido. La lunghezza di una stringa nel file è eccessiva per la colonna del buffer.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|La percentuale %2!ld! non è valida per la proprietà "%1". Deve essere un valore compreso nell'intervallo da 0 a 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|Il numero di righe %2!ld! non è valido per la proprietà "%1". Deve essere maggiore di 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|All'adattatore è stata richiesta la scrittura di una stringa lunga %1!I64d! byte, ma tutti i dati nel loro complesso devono avere una lunghezza inferiore a 4294967295 byte.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|Nessun mapping eseguito tra input e output. Per "%1" è necessario eseguire il mapping di almeno una colonna di input a una colonna di output.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|La conversione da "%1" con tabella codici %2!d! a "%3" con tabella codici %4!d! non è supportata.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|Il mapping della colonna di metadati esterna per %1 non è valido.  L'ID della colonna di metadati esterna non può essere zero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|Per %1 è stato definito un mapping a una colonna di metadati esterna che non esiste.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Errore durante la scrittura di dati oggetto long di tipo DT_TEXT, DT_NTEXT o DT_IMAGE nel buffer dell'attività Flusso di dati per la colonna "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Impossibile aprire un set di righe per "%1". Controllare che l'oggetto esista nel database.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Impossibile accedere alla variabile "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|Impossibile trovare la gestione connessione "%1". Un componente non è riuscito a trovare la gestione connessione nella raccolta Connections.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|Impossibile eseguire l'aggiornamento dalla versione "%1" alla versione %2!d! .|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|Un valore in una colonna di input è troppo grande per essere archiviato nell'oggetto ADODB.Recordset.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Impossibile convertire le colonne "%1" e "%2" dal tipo di dati stringa Unicode al tipo stringa non Unicode.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|La variabile "%1" specificata dalla proprietà VariableName non è valida. È necessario un nome di variabile valida in cui scrivere.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|La variabile "%1" specificata dalla proprietà VariableName non è di tipo Integer. Modificare la variabile impostando il tipo VT_I4, VT_UI4, VT_I8 o VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|Nessuna colonna specificata per consentire al componente di avanzare nel file.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|La proprietà IsSorted di "%1" è impostata su TRUE, ma le posizioni SortKeyPosition per tutte le colonne di output sono zero. Impostare la proprietà IsSorted su FALSE oppure selezionare almeno una colonna di output con valore SortKeyPosition diverso da zero.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|I metadati di "%1" non corrispondono ai metadati della colonna di input.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|Impossibile individuare, bloccare o impostare il valore della variabile specificata.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|Impossibile elaborare la colonna "%1". Per tale colonna sono impostate più tabelle codici (%2!d! e %3!d!).|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|Impossibile inserire la colonna "%1". La conversione tra i tipi %2 e %3 non è supportata.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Impossibile convertire la colonna "%1" dal tipo di dati stringa Unicode al tipo stringa non Unicode.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1 non è in grado di trovare la colonna con LineageID %2!ld! nel buffer di input.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1 non è in grado di recuperare le informazioni per la colonna %2!lu! dal buffer di input.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|%1 non è in grado di recuperare le informazioni per la colonna "%2!lu!" dal buffer di copia.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1 non è in grado di registrare un tipo di buffer per il buffer di copia.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1 non è in grado di creare un buffer in cui copiare i dati per l'ordinamento.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|Chiamata Read non riuscita dal client DataReader oppure DataReader chiuso.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|Il comando SQL non ha restituito alcuna informazione sulla colonna.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1 non è stato in grado di recuperare informazioni sulla colonna per il comando SQL. Si è verificato l'errore seguente: %2.|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|Non è stato specificato alcun nome di tabella di origine.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|La posizione dell'indice della cache %1!d! non è valida. Per le colonne non dell'indice", la posizione dell'indice deve essere 0. Per le colonne dell'indice, la posizione dell'indice deve essere un numero positivo sequenziale.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|La posizione dell'indice %1!d! è duplicata. Per le colonne non dell'indice", la posizione dell'indice deve essere 0. Per le colonne dell'indice, la posizione dell'indice deve essere un numero positivo sequenziale.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|È necessario specificare almeno una colonna dell'indice per la gestione connessione della cache. Per specificare una colonna dell'indice, impostare la proprietà Index Position della colonna della cache.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Le posizioni dell'indice della cache devono essere contigue. Per le colonne non dell'indice", la posizione dell'indice deve essere 0. Per le colonne dell'indice, la posizione dell'indice deve essere un numero positivo sequenziale.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|Impossibile impostare la proprietà "%1" per "%2". La proprietà non è supportata dall'oggetto specificato. Controllare il nome, l'ortografia e la combinazione di maiuscole/minuscole della proprietà.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|Impossibile modificare il tipo della proprietà dal tipo impostato dal componente.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Errore dell'output con ID %1!d! durante l'inserimento. Il nuovo output non è stato creato.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Impossibile eliminare l'ID di output %1!d! dalla raccolta di output.  È possibile che l'ID non sia valido oppure che rappresenti l'output predefinito o l'output degli errori.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Impossibile impostare la proprietà "%1" per "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Impossibile impostare il tipo di %1 sul tipo: "%2", lunghezza: %3!d!, precisione: %4!d!, scala: %5!d!, tabella codici: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|Nel componente sono stati rilevati più output degli errori e può esisterne uno solo.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|Impossibile impostare la proprietà per una colonna di output.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|Impossibile modificare il tipo di dati per "%1" nell'errore "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|Impossibile impostare la proprietà IsSorted di "%1" su TRUE perché non è un output di origine. Per un output di origine il valore SynchronousInputID è zero.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|Impossibile impostare la proprietà SortKeyPosition di "%1" su un valore diverso da zero perché "%2" non è un output di origine. La proprietà SortKeyPosition della colonna di output "nomecolonna" (ID) non può essere impostata su un valore diverso da zero perché l'output corrispondente "nomeoutput" (ID) non è un output di origine.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|Impossibile impostare la proprietà ComparisonFlags su un valore diverso da zero per "%1" perché "%2" non è un output di origine. La proprietà ComparisonFlags della colonna di output "nomecolonna" (ID) non può essere impostata su un valore diverso da zero perché l'output corrispondente "nomeoutput" (ID) non è un output di origine.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|I flag di confronto per "%1" devono essere zero perché il tipo non è string. La proprietà ComparisonFlags può essere impostata solo su valori diversi da zero per le colonne di tipo string.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|Impossibile impostare la proprietà ComparisonFlags per "%1" su un valore diverso da zero perché la relativa proprietà SortKeyPosition è impostata su zero. La proprietà ComparisonFlags di una colonna di output può essere impostata solo su valori diversi da zero se anche la proprietà SortKeyPosition è diversa da zero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|la proprietà è di sola lettura.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|Per %1 è stato impostato un valore di tipo di dati non valido (%2!ld!).|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|Per "%1" è necessario impostare una tabella codici ma è stato passato il valore zero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|La lunghezza di "%1" non è valida. Deve essere compresa tra %2!ld! e %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|La scala di "%1" non è valida. Deve essere compresa tra %2!ld! e %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|La precisione di "%1" non è valida. Deve essere compresa tra %2!ld! e %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|Il valore impostato per la lunghezza, la precisione, la scala o la tabella codici di "%1" è diverso da zero, ma il tipo di dati richiede che tale valore sia zero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1 non consente l'impostazione di proprietà del tipo di dati per la colonna di output.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|"%1" contiene un tipo di dati non validi. "%1" è un tipo di colonna di errori speciale e l'unico tipo di dati valido è DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|Il componente non fornisce descrizioni dei codici di errore.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|Il codice di errore specificato non è associato a questo componente.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|Un troncamento ha causato il reindirizzamento della riga, in base alle impostazioni delle disposizioni per i troncamenti.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|"%1!s!" non è in grado di impostare in lettura/scrittura la colonna con ID di derivazione %2!d! perché tale tipo di utilizzo non è consentito per la colonna. Si è tentato di modificare il tipo di utilizzo di una colonna di input impostandolo sul tipo UT_READWRITE non supportato da questo componente.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|%1 ha rifiutato il tipo di utilizzo richiesto della colonna di input con ID di derivazione %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1" non ha potuto apportare la modifica richiesta alla colonna di input con ID di derivazione %2!d!. Richiesta non riuscita con codice di errore 0x%3!8.8X!. L'errore specificato si è verificato durante il tentativo di impostazione del tipo di utilizzo di una colonna di input.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Tentativo di impostazione delle proprietà del tipo di dati per "%1" non riuscito con codice di errore 0x%2!8.8X!. L'errore si è verificato durante il tentativo di impostazione di una o più proprietà del tipo di dati per la colonna di output.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|Impossibile recuperare i metadati per "%1". Verificare che il nome di oggetto sia corretto e che l'oggetto esista.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|Impossibile eseguire il mapping della colonna di output a una colonna di metadati esterna.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|La variabile %1 deve essere di tipo "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1 non consente l'impostazione di proprietà del tipo di dati per le colonne di metadati esterne.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|L'ID %1!lu! non corrisponde a un ID di input o di output. L'ID specificato deve essere l'ID di input o l'ID di output a cui viene associata la raccolta dei metadati esterna.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|La raccolta dei metadati esterna in "%1" è contrassegnata come non utilizzata. Impossibile eseguire operazioni su tale raccolta.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1 è un output sincrono. Impossibile recuperare il tipo di buffer per un output sincrono.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|La colonna di input "%1" deve essere di sola lettura. Il tipo di utilizzo della colonna di input è diverso da sola lettura e ciò non è consentito.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|Per "%1" manca la proprietà richiesta "%2". La proprietà personalizzata specificata deve essere impostata per l'oggetto.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|L'output %1 non supporta l'assegnazione della proprietà "%2", ma attualmente tale proprietà è assegnata.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1 deve essere presente nel gruppo di esclusioni %2!d!. Tutti gli output devono essere inseriti nel gruppo di esclusioni specificato.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|La proprietà "%1" è vuota. La proprietà non può essere vuota.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|Impossibile allocare memoria per l'espressione "%1". Errore di memoria insufficiente durante la creazione di un oggetto interno per la memorizzazione dell'espressione.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Impossibile analizzare l'espressione "%1". Espressione non valida o memoria insufficiente.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Impossibile calcolare l'espressione "%1". Codice di errore: 0x%2!8.8X!. È possibile che l'espressione contenga errori non individuabili in fase di analisi, come una divisione per zero, oppure che la memoria sia insufficiente.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Impossibile allocare memoria per gli oggetti Expression. Errore di memoria insufficiente durante la creazione della matrice di puntatori all'oggetto Expression.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|Errore di %1 con codice 0x%2!8.8X! durante la creazione dello strumento di gestione delle espressioni.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|L'espressione "%1" non è booleana. Il tipo di risultato dell'espressione deve essere booleano.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|L'espressione "%1" in "%2" non è valida.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|Impossibile trovare una colonna del file di input corrispondente per la colonna "%1" (%2!d!). Impossibile trovare nel file il nome della colonna di input o il nome della colonna di output.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Tentativo di impostazione della colonna di risultati per l'espressione "%1" in %2 non riuscito con codice di errore 0x%3!8.8X!. Impossibile determinare la colonna di input o di output destinata a ricevere il risultato dell'espressione oppure non è possibile eseguire il cast del risultato dell'espressione nel tipo della colonna.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|%1 non è riuscito a recuperare l'ID delle impostazioni locali dal pacchetto.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|Il formato della stringa di mapping dei parametri non è corretto.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|IL comando SQL richiede %1!d! parametri, ma il mapping dei parametri include solo %2!d! parametri.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|Il comando SQL richiede un parametro denominato "%1" non disponibile nel mapping dei parametri.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|Esistono più colonne di origine dei dati con il nome "%1".  I nomi delle colonne di origine dei dati devono essere univoci.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|Esiste una colonna di origine dei dati senza nome.  Tutte le colonne di origine dei dati devono avere un nome.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|Un componente è disconnesso dal layout.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|L'ID di un componente del layout non è valido.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|Numero di input non valido per un componente.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|Numero di output non valido per un componente.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|Un componente non include alcun input o output.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|Memoria insufficiente per allocare un elenco delle colonne manipolate dal componente.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|La colonna di output "%1" (%2!d!) fa riferimento alla colonna di input con ID di derivazione %3!d!. Impossibile trovare un input con tale ID di derivazione.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|Almeno una colonna di input deve essere contrassegnata come chiave di ordinamento, ma non è stata trovata alcuna chiave.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Entrambe le colonne "%1" (%2!d!) e "%3" (%4!d!) sono contrassegnate con il peso della chiave di ordinamento %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|Il componente potrà eseguire la modifica richiesta dei metadati solo dopo la risoluzione del problema di convalida.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|Impossibile aggiungere un input alla raccolta degli input.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|Impossibile aggiungere un output alla raccolta degli output.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|Impossibile eliminare un input dalla raccolta degli input.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|Impossibile rimuovere un output dalla raccolta degli output.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|Impossibile modificare il tipo di utilizzo della colonna.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|%1 deve essere in lettura/scrittura per supportare la proprietà personalizzata "%2". La proprietà personalizzata specificata esiste per la colonna di input o output, ma la colonna non è in lettura/scrittura. Rimuovere la proprietà o impostare la colonna in lettura/scrittura.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1 è in lettura/scrittura e deve avere la proprietà personalizzata "%2". Aggiungere la proprietà o rimuovere l'attributo di lettura/scrittura dalla colonna.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|Impossibile eliminare la colonna. Il componente non consente l'eliminazione di colonne da questo input o output.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|Il componente non consente l'aggiunta di colonne a questo input o output.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|Impossibile trovare la connessione "%1". Verificare che per la gestione connessione sia disponibile una connessione con tale nome.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|Impossibile trovare la gestione di connessione di run-time con ID "%1". Verificare che nella raccolta delle gestioni connessioni sia presente una gestione connessione con tale ID.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|Codice di errore SSIS DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  Chiamata del metodo AcquireConnection alla gestione connessione "%1" non riuscita con codice di errore 0x%2!8.8X!.  Possono essere presenti ulteriori messaggi di errore prima di questo con informazioni aggiuntive sui motivi dell'esito negativo della chiamata del metodo AcquireConnection.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|La connessione acquisita dalla gestione connessione "%1" non è valida.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|Il tipo della gestione connessione "%1" non è corretto.  Il tipo richiesto è "%2". Il tipo disponibile per il componente è "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Impossibile acquisire una connessione gestita dalla gestione connessione di run-time.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|Impossibile creare un input per inizializzare la raccolta degli input.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|Impossibile creare un output per inizializzare la raccolta degli output.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Impossibile scrivere nel file "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|La gestione connessione "%1" ha restituito un oggetto di tipo non corretto dal metodo AcquireConnection.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|La proprietà "%3" è necessaria per la colonna di input "%1" (%2!d!) ma non è disponibile. La proprietà mancante deve essere aggiunta.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|La colonna "%1" è di sola lettura, ma non esistono riferimenti da altre colonne. Le colonne senza riferimenti non sono consentite.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|"%1" fa riferimento all'ID di colonna %2!d! e tale colonna non è disponibile nell'input. È presente un riferimento che punta a una colonna inesistente.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|"%1" fa riferimento a "%2" e tale colonna non è di tipo BLOB.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1" fa riferimento all'ID di colonna di output %2!d! e tale colonna non è disponibile nell'output.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Impossibile leggere dal file "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|L'input per una trasformazione Dimensione a modifica lenta deve includere almeno una colonna di tipo fisso, modificabile o cronologico. Verificare che per almeno una colonna sia impostato l'attributo fisso, modificabile o cronologico.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|La proprietà ColumnType di "%1" non è valida. Il valore corrente non è compreso nell'intervallo dei valori accettabili.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|Impossibile eseguire il mapping della colonna di input "%1" alla colonna esterna "%2" perché i tipi di dati sono diversi. La trasformazione Dimensione a modifica lenta non consente il mapping tra colonne di tipi diversi, con l'eccezione dei tipi DT_STR e DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|Il tipo di dati per "%1" è DT_NTEXT e non è supportato per i file ANSI. Utilizzare in alternativa il tipo di dati DT_TEXT e convertire i dati al tipo DT_NTEXT utilizzando il componente per la conversione dei dati.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|Il tipo di dati per "%1" è DT_TEXT e non è supportato per i file Unicode. Utilizzare in alternativa il tipo di dati DT_NTEXT e convertire i dati al tipo DT_TEXT utilizzando il componente per la conversione dei dati.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|Il tipo di dati per "%1" è DT_IMAGE e non è supportato. Utilizzare in alternativa il tipo di dati DT_TEXT o DT_NTEXT convertire i dati dal o al tipo DT_IMAGE utilizzando il componente per la conversione dei dati.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|Il formato "%1" non è supportato dalla gestione connessione file flat. I formati supportati sono Delimited, FixedWidth, RaggedRight e Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|"%1" dovrebbe contenere un nome di file ma non è di tipo string.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Errore causato da impostazioni di proprietà in conflitto. Per "%1" sia la proprietà AllowAppend che la proprietà ForceTruncate sono impostate su TRUE. Non è consentito impostare entrambe le proprietà su TRUE. Impostare una delle due proprietà su FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 fa riferimento all'ID di colonna %2!d!, ma esiste già un riferimento a tale colonna da %3. Rimuovere uno dei due riferimenti alla colonna.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|Nessuna gestione connessione assegnata a %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 fa riferimento alla colonna di output con ID %2!d!, ma esiste già un riferimento a tale colonna da %3.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|Nessuna colonna di input fa riferimento a "%1". Per ogni colonna di output deve esistere un riferimento da una sola colonna di input.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|"%1" fa riferimento a "%2" e il tipo di tale colonna non è corretto. Il tipo deve essere DT_TEXT, DT_NTEXT o DT_IMAGE. Un riferimento punta a una colonna che deve essere di tipo BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|"%1" dovrebbe contenere un nome di file ma non è di tipo string.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|La proprietà ExpectBOM "%1" è impostata su TRUE per %2, ma la colonna non è di tipo NT_NTEXT. La proprietà ExpectBOM specifica che la trasformazione Imposta colonna prevede un indicatore per l'ordine dei byte (BOM). Impostare la proprietà ExpectBOM su FALSE o cambiare il tipo di dati della colonna di output in DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Le colonne di output dei dati devono essere di tipo DT_TEXT, DT_NTEXT o DT_IMAGE. La colonna di output dei dati può essere impostata solo su un tipo BLOB.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|Se la proprietà FailOnFixedAttributeChange è impostata su TRUE, la trasformazione genererà un errore se viene rilevata la modifica di un attributo fisso. Per inviare righe all'output di tipo Attributo fisso, impostare la proprietà FailOnFixedAttributeChange su FALSE.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|La trasformazione Ricerca non è riuscita a recuperare alcuna riga. Questo errore della trasformazione si verifica quando la proprietà FailOnLookupFailure è impostata su TRUE e non vengono recuperate righe.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|L'input di una trasformazione Dimensione a modifica lenta deve includere almeno una colonna di tipo Chiave. Impostare il tipo Chiave per almeno una colonna.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Impossibile trovare la colonna esterna con nome "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|La colonna Indicatore membro derivato "%1" deve essere di tipo DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|Il valore della disposizione per le righe con errori per %1 deve essere impostato su RD_NotUsed.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|Il valore della disposizione per le righe con troncamenti per %1 deve essere impostato su RD_NotUsed.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Impossibile trovare la colonna di input con ID di derivazione %1!d! richiesta dalla colonna di output con ID %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Tipo di dati di output non valido per il tipo di aggregazione specificato nella colonna di output con ID %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Tipo di dati di input non valido per %1 utilizzato per l'aggregazione specificata in %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|I tipi di dati della colonna di input con ID di derivazione %1!d! e della colonna di output con ID %2!d! non corrispondono.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Impossibile ottenere l'handle del buffer di input per l'input con ID %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Impossibile ottenere l'handle del buffer di output per l'output con ID %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Impossibile trovare la colonna con ID di derivazione %1!d! nel buffer di output.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Impossibile trovare la colonna con ID di derivazione %1!d! nel buffer di input.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|Il numero di colonne di output per %1 non può essere zero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|Il numero di colonne nella gestione connessione file flat deve essere uguale al numero di colonne nell'adattatore file flat. Il numero di colonne per la gestione connessione file flat è %1!d!, mentre il numero di colonne per l'adattatore file flat è %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|Impossibile trovare la colonna"%1" con indice %2!d! nella gestione connessione file flat in corrispondenza dell'indice %3!d! nella raccolta delle colonne dell'adattatore file flat.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|È stato già eseguito il mapping della colonna di metadati esterna con ID %1!d! a %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|La trasformazione ha individuato una colonna chiave più grande di %1!u! caratteri.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|La trasformazione ha individuato un valore di risultato più lungo di %1!u! byte.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Impossibile allocare memoria.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Impossibile allocare memoria.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Impossibile allocare memoria.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Impossibile allocare memoria.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Impossibile allocare memoria.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Impossibile allocare memoria.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Impossibile allocare memoria.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Impossibile allocare memoria.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|Nessun riferimento alla colonna di input "%1".|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|La trasformazione Ordinamento non ha potuto creare un pool di thread con %1!d! thread. Memoria insufficiente.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|La trasformazione Ordinamento non ha potuto accodare un elemento di lavoro nel pool di thread. Memoria insufficiente.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|Arresto di un thread di lavoro nella trasformazione Ordinamento con codice di errore 0x%1!8.8X!. Errore irreversibile durante l'ordinamento di un buffer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|Il valore MaxThreads è %1!ld! e dovrebbe essere compreso tra 1 e %2!ld!, inclusi, oppure -1 per utilizzare il numero di CPU come impostazione predefinita.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Impossibile caricare da XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|Impossibile salvare in XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Impossibile convertire il valore "%1" in un tipo Integer.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Impossibile convertire il valore "%1" in un tipo booleano.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Errore di caricamento in prossimità dell'oggetto con ID %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|Il valore "%1" non è valido per l'attributo "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|Il valore "%1" non è valido per l'attributo "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|Il valore "%1" non è valido per l'attributo "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|Per %1 non è stato definito un mapping a una colonna di output.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|Mapping non valido per %1.  Nel componente non esiste una colonna di output con ID %2!ld!.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|Per %1 è stato definito un mapping a una colonna di output per la quale esiste già un mapping in questo input.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Impossibile convertire la colonna di input con ID di derivazione %1!ld! nel tipo DT_WSTR a causa dell'errore 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Impossibile trovare l'oggetto di riferimento con ID %1!d! nel pacchetto.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Impossibile leggere una proprietà di persistenza necessaria per il modulo pipelinexml. La pipeline non ha fornito la proprietà.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|Il valore "%1" non è valido per l'attributo "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Impossibile recuperare la proprietà personalizzata "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|Impossibile trovare nella raccolta delle colonne di input una colonna di input con ID di derivazione %1!d!, a cui si fa riferimento nella proprietà personalizzata ParameterMap con il parametro alla posizione numero %2!d!.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Impossibile individuare la colonna di riferimento "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|Tipi di dati non compatibili per_%1 e la colonna di riferimento denominata "%2".|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|L'istruzione SQL con parametri restituisce metadati non corrispondenti all'istruzione SQL principale.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|L'istruzione SQL con parametri contiene un numero di parametri non corretto. Previsti %1!d!, trovati %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|Il tipo di dati di %1 non consente il join.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|Il tipo di dati di %1 non consente la copia.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|Il tipo di dati di %1 non è supportato. Il tipo deve essere DT_STR o DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|Il tipo di dati di %1 non è supportato. Deve essere DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|Il tipo di dati di %1 non è supportato. Deve essere DT_STR, DT_WSTR, DT_TEXT o DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|La trasformazione Ordinamento non è in grado di creare un evento per comunicare con i relativi thread di lavoro. Handle di sistema insufficienti per la trasformazione Ordinamento.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|La trasformazione Ordinamento non è in grado di creare un thread di lavoro. Memoria insufficiente per la trasformazione Ordinamento.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|La trasformazione Ordinamento non è riuscita a confrontare la riga %1!d! nel buffer con ID %2!d! con la riga %3!d! nel buffer con ID %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|Numero di colonne insufficiente nei metadati di riferimento per la trasformazione Ricerca. Controllare la proprietà SQLCommand. L'istruzione SELECT deve restituire almeno una colonna.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Impossibile allocare memoria per una matrice di strutture ColumnInfo.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Impossibile allocare memoria per una matrice di strutture ColumnPair.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Impossibile allocare memoria per una matrice di strutture BUFFCOL per la creazione di un'area di lavoro principale.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Impossibile creare un buffer per l'area di lavoro principale.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Impossibile allocare memoria per la tabella hash.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Impossibile allocare memoria per creare un heap per i nodi hash.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Impossibile allocare memoria per un heap di nodo hash.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Impossibile creare un heap per i nodi LRU. Memoria insufficiente.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Impossibile allocare memoria per l'heap del nodo LRU. Memoria insufficiente.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Errore OLE DB durante il caricamento dei metadati della colonna. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|Errore OLE DB durante il recupero del set di righe. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|Errore OLE DB durante il popolamento della cache interna. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|Errore OLE DB durante l'associazione dei parametri. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|Errore OLE DB durante la creazione delle associazioni. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|Caso non valido rilevato in un'istruzione switch durante la fase di esecuzione.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Impossibile allocare memoria per una nuova riga per il buffer dell'area di lavoro principale. Memoria insufficiente.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|Errore OLE DB durante il recupero del set di righe con parametri. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|Errore OLE DB durante il recupero della riga con parametri. Controllare le proprietà SQLCommand e SqlCommandParam.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Impossibile allocare memoria per una nuova riga per il buffer dell'area di lavoro principale. Memoria insufficiente.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Impossibile creare un buffer per l'area di lavoro principale.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Impossibile allocare memoria per la tabella hash.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Impossibile allocare memoria per creare un heap per i nodi hash.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Impossibile allocare memoria per l'heap del nodo hash.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Impossibile allocare memoria per creare un heap per i nodi CountDistinct.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Impossibile allocare memoria per l'heap del nodo CountDistinct.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Impossibile allocare memoria per creare un heap per le catene CountDistinct.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Impossibile allocare memoria per la tabella hash CountDistinct.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Impossibile allocare memoria per una nuova riga per il buffer dell'area di lavoro CountDistinct.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Impossibile creare un buffer per l'area di lavoro CountDistinct.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Impossibile allocare memoria per la matrice Collapse CountDistinct.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Impossibile allocare memoria per le catene CountDistinct.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Metadati non corrispondenti per le colonne con ID di derivazione %1!d! e %2!d! . La colonna di input di cui è stato eseguito il mapping a una colonna di output per la trasformazione Copia/Mapping non dispone degli stessi metadati (tipo di dati, precisione, scala, lunghezza o tabella codici).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|Il mapping della colonna di output con ID di derivazione "%1!d!" a una colonna di input è stato eseguito in modo non corretto. La proprietà CopyColumnId della colonna di output non è corretta.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Impossibile recuperare dati long per la colonna "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Per una colonna sono stati recuperati dati long ma non è possibile aggiungerli al buffer dell'attività Flusso di dati.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|L'output "%1" (%2!d!) include colonne di output ma gli output multicast non dichiarano colonne. Il pacchetto è danneggiato.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Impossibile caricare una risorsa localizzata con ID %1!d!. Verificare che il file RLL sia disponibile.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Impossibile acquisire l'interfaccia Events. È stata passata un'interfaccia Events non valida al modulo del flusso di dati per salvare le informazioni sugli eventi in modo persistente nel codice XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|Errore durante l'impostazione di un oggetto percorso durante il caricamento del file XML.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Errore durante l'impostazione dell'oggetto di input durante il caricamento del file XML.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Errore durante l'impostazione dell'oggetto di output durante il caricamento del file XML.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Errore durante l'impostazione dell'oggetto colonna di input durante il caricamento del file XML.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Errore durante l'impostazione dell'oggetto colonna di output durante il caricamento del file XML.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Errore durante l'impostazione dell'oggetto proprietà durante il caricamento del file XML.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Errore durante l'impostazione dell'oggetto connessione durante il caricamento del file XML.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Mancano colonne speciali specifiche della trasformazione o i tipi delle colonne non sono corretti.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|La trasformazione Raggruppamento fuzzy non è riuscita a creare le tabelle e funzioni di accesso richieste.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|La trasformazione Raggruppamento fuzzy non è riuscita a copiare l'input.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|La trasformazione Raggruppamento fuzzy non è riuscita a generare gruppi.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|Errore imprevisto nella trasformazione Raggruppamento fuzzy durante l'applicazione delle impostazioni della proprietà '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|La trasformazione Raggruppamento fuzzy non è riuscita a selezionare una riga di dati canonica da utilizzare per la standardizzazione dei dati.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|La trasformazione Raggruppamento fuzzy non supporta colonne di input di tipo IMAGE, TEXT o NTEXT.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|Nella colonna "%1" (%2!d!) è specificata una corrispondenza fuzzy, ma il tipo di dati della colonna non è DT_STR o DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|Si è verificato un errore di pipeline per la trasformazione Raggruppamento fuzzy. Codice di errore restituito: 0x%1!8.8X!: "%2".|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|La tabella codici %1!d! specificata nella colonna "%2" (%3!d!) non è supportata.  È prima necessario convertire la colonna nel tipo DT_WSTR, operazione che è possibile eseguire inserendo una trasformazione Conversione dati prima di questa.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Errore durante l'impostazione del flag di fine dati per il buffer che indirizza l'output "%1" (%2!d!).|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|Impossibile clonare il buffer di input. Condizione di memoria insufficiente o errore interno.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|La colonna "%1" richiede che i caratteri Katakana e Hiragana vengano generati contemporaneamente.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|La colonna "%1" richiede che i caratteri in cinese semplificato e in cinese tradizionale vengano generati contemporaneamente.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|La colonna "%1" richiede che le operazioni generino sia caratteri a larghezza intera che a metà larghezza.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|La colonna "%1" combina le operazioni sui caratteri giapponesi con operazioni per i caratteri cinesi.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|La colonna "%1" combina le operazioni sui caratteri cinesi con operazioni su maiuscole e minuscole.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|La colonna "%1" combina le operazioni sui caratteri giapponesi con operazioni su maiuscole e minuscole.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|La colonna "%1" esegue il mapping della colonna sia ai caratteri maiuscoli che a quelli minuscoli.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|La colonna "%1" combina i flag diversi da Maiuscolo e Minuscolo con l'operazione di conversione da maiuscole a minuscole (e viceversa) basata sulla lingua.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|Impossibile eseguire il mapping del tipo di dati della colonna "%1" come specificato.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|La versione (%1) dell'indice delle corrispondenze preesistente "%2" non è supportata. La versione prevista è "%3". Questo errore si verifica se la versione persistente nei metadati dell'indice non corrisponde alla versione per la quale è stato compilato il codice corrente. Per risolvere il problema, ricompilare l'indice con la versione corrente del codice.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|La tabella "%1" non rappresenta un indice delle corrispondenze preesistente valido. Questo errore si verifica quando non è possibile caricare il record dei metadati dall'indice preesistente specificato.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Impossibile leggere l'indice delle corrispondenze preesistente "%1" specificato.  Codice di errore OLE DB: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|Nessuna colonna di input con un join valido a una colonna della tabella di riferimento.  Verificare che esista almeno un join definito con le proprietà delle colonne di input JoinToReferenceColumn e JoinType.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|L'indice delle corrispondenze preesistente specificato "%1" non è stato compilato in origine con informazioni di corrispondenze fuzzy per la colonna "%2".  È necessario ricompilarlo per includere tali informazioni. Questo errore si verifica quando l'indice viene compilato con una colonna che non è una colonna di join fuzzy.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|Il nome "%1" specificato per la proprietà "%2" non è un nome di identificatore SQL valido. Questo errore si verifica se il nome della proprietà non è conforme alle specifiche per i nomi di identificatore SQL validi.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|Il valore della proprietà di soglia MinSimilarity nella trasformazione Ricerca fuzzy deve essere maggiore o uguale a 0,0 ma minore di 1,0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|Il valore "%1" per la proprietà "%2" non è valido.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|La ricerca fuzzy specificata tra la colonna di input "%1" e la colonna di riferimento "%2" non è valida. I join fuzzy sono supportati solo tra colonne stringa di tipo DT_STR e DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|Le colonne per la ricerca esatta, "%1" e "%2", non hanno gli stessi tipi di dati oppure sono di tipi stringa non confrontabili. I join esatti sono supportati tra colonne con tipi di dati uguali o con combinazioni dei tipi DT_STR e DT_WSTR.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|Le colonne per la copia, "%1" e "%2", non hanno gli stessi tipi di dati oppure sono di tipi stringa non facilmente convertibili. La copia da colonne di riferimento a colonne di output è supportata solo tra colonne con tipi di dati uguali oppure con combinazioni dei tipi DT_STR e DT_WSTR. Non sono supportati altri tipi.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|Le colonne pass-through, "%1" e "%2", non hanno gli stessi tipi di dati. Solo le colonne con tipi di dati uguali sono supportate come colonne pass-through dall'input all'output.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Impossibile individuare la colonna di riferimento "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|Per una colonna di output è necessario specificare una sola delle proprietà CopyColumn e PassThruColumn. Questo errore si verifica quando né la proprietà CopyColumn né la proprietà PassThruColumn oppure entrambe le proprietà CopyColumn e PassThruColumn sono impostate su valori non vuoti.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|L'ID di derivazione di origine '%1!d!' specificato per la proprietà '%2' nella colonna di output '%3' non è stato trovato nella raccolta delle colonne di input. Questo errore si verifica quando l'ID di colonna di input specificato per una colonna di output come colonna pass-through non è disponibile nel set degli input.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|Impossibile trovare la colonna "%1" nell'indice preesistente "%2" nella tabella/query di riferimento. Questo errore si verifica quando si apportano modifiche allo schema o alla query della tabella di riferimento dopo la compilazione dell'indice delle corrispondenze preesistente.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|Il componente ha rilevato un token più grande di 2147483647 caratteri.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|Impossibile accodare il file di output. Il nome della colonna "%1" corrisponde, ma il tipo della colonna nel file è %2 e il tipo della colonna di input è %3. I metadati per la colonna non corrispondono per il tipo di dati.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|Impossibile accodare il file di output. Il nome della colonna "%1" corrisponde, ma la lunghezza massima della colonna nel file è %2!d! mentre la lunghezza massima della colonna di input è %3!d!. I metadati per la colonna non corrispondono per la lunghezza.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|Impossibile accodare il file di output. Il nome della colonna "%1" corrisponde, ma la tabella codici della colonna nel file è %2!d! e la tabella codici della colonna di input è %3!d!. I metadati per la colonna non corrispondono per la tabella codici.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|Impossibile accodare il file di output. Il nome della colonna "%1" corrisponde, ma la precisione della colonna nel file è %2!d! e la precisione della colonna di input è %3!d!. I metadati per la colonna non corrispondono per la precisione.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|Impossibile accodare il file di output. Il nome della colonna "%1" corrisponde, ma la scala della colonna nel file è %2!d! e la scala della colonna di input è %3!d!.  I metadati per la colonna non corrispondono per la scala.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Impossibile determinare il nome e la versione del DBMS in "%1". Questo errore si verifica se IDBProperties nella connessione non restituisce le informazioni necessarie per verificare il nome e la versione del DBMS.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|Il tipo o la versione di DBMS di "%1" non è supportato.  È necessaria una connessione a Microsoft SQL Server versione 8.0 o successiva. Questo errore si verifica se IDBProperties nella connessione non restituisce una versione corretta.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1 è una colonna speciale di output degli errori e non può essere eliminata.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|Il tipo di dati specificato per la colonna "%1" non è il tipo previsto "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|Impossibile trovare nella raccolta delle colonne di input la colonna di input con ID di derivazione "%1" a cui fa riferimento la proprietà "%2" nella colonna di output "%3".|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|Per la colonna di input "%1" a cui fa riferimento la proprietà "%2" nella colonna di output "%3" è necessario che la proprietà ToBeCleaned sia impostata su True e che sia impostato un valore valido per la proprietà ExactFuzzy.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|La tabella di riferimento '%1' non include un indice cluster su una colonna Identity di tipo Integer, come richiesto se la proprietà 'CopyRefTable' è impostata su FALSE. Se la proprietà CopyRefTable è false, la tabella di riferimento deve includere un indice cluster su una colonna Identity di tipo Integer.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|La tabella di riferimento '%1' contiene una colonna Identity di tipo non Integer e ciò non è supportato. Utilizzare una vista della tabella senza la colonna '%2'.  Questo errore si verifica perché quando si crea una copia della tabella di riferimento viene aggiunta una colonna Identity di tipo Integer ed è consentita una sola colonna Identity per tabella.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|Impossibile specificare contemporaneamente sia la proprietà MatchContribution che informazioni di gerarchia. Ciò non è consentito perché entrambe le proprietà rappresentano fattori di ponderazione per il punteggio.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|I livelli nella gerarchia devono essere numeri univoci. Sono valori validi per i livelli della gerarchia i numeri interi maggiori o uguali a 1. Minore è il numero, più basso è il livello della colonna nella gerarchia. Il valore predefinito è 0 che indica che la colonna non fa parte della gerarchia. Non sono consentiti sovrapposizioni o gap.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|Nessuna colonna definita per il raggruppamento fuzzy.  È necessario che esista almeno una colonna di input con le impostazioni di proprietà ToBeCleaned=true e ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|La colonna con ID '%1!d!' non è valida per motivi non determinati.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|Il tipo di dati della colonna '%1' non è supportato.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|La lunghezza della colonna di output '%1' è minore della lunghezza della colonna di origine corrispondente '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|Deve esistere una sola colonna di input.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|Devono esistere esattamente due colonne di output.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|Il tipo di dati della colonna di input può essere solo DT_WSTR o DT_NTEXT.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|Il tipo di dati della colonna di output [%1!d!] può essere solo '%2'.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|Il tipo di dati della colonna di riferimento può essere solo DT_STR o DT_WSTR.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|Errore durante l'individuazione della colonna di riferimento '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|Il Tipo di termine della trasformazione può essere solo WordOnly, PhraseOnly o WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|Il valore di Soglia frequenza non deve essere minore di '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|Il valore di Lunghezza massima termine non deve essere minore di '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Numero di colonne insufficiente nei metadati di riferimento per la trasformazione Estrazione termini.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|Errore durante l'allocazione della memoria.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|Errore durante la creazione di un buffer per l'area di lavoro.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|Errore OLE DB durante la creazione delle associazioni.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|Errore OLE DB durante il recupero dei set di righe.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|Errore OLE DB durante il popolamento della cache interna.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|Errore durante l'estrazione dei termini nella riga %1!ld!, colonna %2!ld!. Codice di errore restituito: 0x%3!8.8X!. Per risolvere il problema, rimuovere la colonna dall'input.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|Il numero di candidati per il termine è superiore al limite di 4 GB.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|La tabella, la vista o la colonna di riferimento utilizzata per i termini di esclusione non è valida.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|La lunghezza della colonna stringa '%1' è maggiore di 4000 caratteri.  È necessaria la conversione dal tipo DT_STR al tipo DT_WSTR, pertanto si verificherà un troncamento.  Ridurre la larghezza della colonna oppure utilizzare solo tipi DT_WSTR.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|Non è stata impostata la tabella, la vista o la colonna di riferimento da utilizzare per i termini di esclusione.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|Numero di colonne di output insufficiente per la trasformazione Ricerca termini.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|Il tipo di dati della colonna di riferimento può essere solo DT_STR o DT_WSTR.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|Errore durante l'individuazione della colonna di riferimento '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Numero di colonne insufficiente nei metadati di riferimento per la trasformazione Ricerca termini.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|Errore durante la normalizzazione delle parole.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|Errore durante la creazione di un buffer per l'area di lavoro.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|Errore OLE DB durante la creazione delle associazioni.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|Errore OLE DB durante il recupero dei set di righe.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|Errore OLE DB durante il popolamento della cache interna.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|Errore durante la ricerca dei termini nella riga %1!ld!, colonna %2!ld!. Codice di errore restituito: 0x%3!8.8X!. Per risolvere il problema, rimuovere la colonna dall'input.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|Non è stato eseguito il mapping almeno di una colonna pass-through a una colonna di output.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|Deve esistere una sola colonna di input di cui è stato eseguito il mapping a una colonna di riferimento.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|Il tipo di dati della colonna di input di cui è stato eseguito il mapping a una colonna di riferimento può essere solo DT_NTXT o DT_WSTR.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|Il nome della tabella di riferimento "%1" non è un identificatore SQL valido. Questo errore si verifica quando non è possibile analizzare il nome della tabella dalla stringa di input. È possibile che il nome includa spazi non racchiusi tra virgolette. Verificare che le virgolette siano utilizzate correttamente nel nome.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|Errore durante l'avvio dell'iterazione del filtro dei termini.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|Errore durante il recupero del buffer utilizzato per la memorizzazione dei termini nella cache. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|Si è verificato un errore std::length_error dai contenitori STL.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|Errore durante il salvataggio di parole con caratteri di punteggiatura. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|Errore durante l'elaborazione del termine di riferimento %1!ld!th. Codice di errore restituito: 0x%2!8.8X!. Per risolvere il problema, rimuovere il termine di riferimento dalla tabella di riferimento.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|Errore durante l'ordinamento dei termini di riferimento. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|Errore durante il conteggio dei candidati per il termine. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|La trasformazione Ricerca fuzzy non è riuscita a caricare l'intera tabella di riferimento nella memoria principale come richiesto quando è abilitata la proprietà Exhaustive.  Memoria di sistema insufficiente oppure è stato specificato un limite per MaxMemoryUsage insufficiente per il caricamento della tabella di riferimento.  Impostare MaxMemoryUsage su 0 o aumentare il valore in modo significativo.  In alternativa, disabilitare la proprietà Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|Errore durante l'inizializzazione del motore di Ricerca termini. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|Errore durante l'elaborazione delle frasi. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|Errore durante l'aggiunta di stringhe in un buffer interno. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|Errore durante il salvataggio dei tag delle parti del discorso da un buffer interno. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|Errore durante il conteggio dei candidati per il termine. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|Errore durante l'inizializzazione dell'elaboratore delle parti del discorso. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|Errore durante il caricamento dell'automa a stati finiti. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|Errore durante l'inizializzazione del motore di Estrazione termini. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|Errore durante l'elaborazione in una frase. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|Errore durante l'inizializzazione dell'elaboratore delle parti del discorso. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|Errore durante l'aggiunta di stringhe in un buffer interno. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|Errore durante l'aggiunta di parole a un decodificatore statistico. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|Errore durante la decodifica di una frase. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|Errore durante l'impostazione dei termini di esclusione. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|Errore durante l'elaborazione di un documento nell'input. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|Errore durante il test per stabilire se un punto fa parte di un acronimo. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|Errore durante l'impostazione dei termini di riferimento. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|Errore durante l'elaborazione di un documento nell'input. Codice di errore restituito: 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|Il valore della proprietà %1 è %2!d! e non è consentito.  Il valore deve essere maggiore o uguale a %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|Il valore della proprietà %1 è %2!d! e deve essere minore o uguale al valore %3!d! per la proprietà %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|Errore durante il tentativo di eliminazione dell'indice delle corrispondenze fuzzy esistente denominato "%1". È possibile che la tabella non sia stata creata dalla trasformazione Ricerca fuzzy (o da questa versione di Ricerca fuzzy), che sia danneggiata o che la causa sia un problema di altro tipo. Provare a eliminare manualmente la tabella denominata "%2" o specificare un nome diverso per la proprietà MatchIndexName.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|L'opzione Tipo di punteggio della trasformazione può essere impostata solo su Frequenza o TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|La tabella di riferimento specificata include troppe righe. La trasformazione Ricerca fuzzy opera unicamente con tabelle di riferimento composte da meno di 1 miliardo di righe. Provare a utilizzare una vista più limitata della tabella di riferimento.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Impossibile determinare le dimensioni della tabella di riferimento '%1'.  È possibile che l'oggetto sia una vista e non una tabella.  La trasformazione Ricerca fuzzy non supporta le viste quando CopyReferentaceTable=false.  Verificare che la tabella esista e che CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|Il tipo di dati "%1" dell'attività Flusso di dati SSIS per %2 non è supportato per %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Impossibile impostare le proprietà del tipo di dati per la colonna di output con ID %1!d! nell'output con ID %2!d!. Impossibile trovare l'output o la colonna.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|Impossibile modificare il valore della proprietà personalizzata "%1" in %2.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|Per %1 nell'output non degli errori non esiste una colonna di output corrispondente nell'output degli errori.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|Per %1 nell'output degli errori non esiste una colonna di output corrispondente nell'output non degli errori.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|Per %1 nell'output degli errori esistono proprietà che non corrispondono alle proprietà della colonna di origine dei dati corrispondente.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|Impossibile modificare il tipo di dati delle colonne di output su %1, ad eccezione delle colonne DT_WSTR e DT_NTEXT.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|Il tipo di dati di "%1" non corrisponde al tipo di dati "%2" della colonna di origine "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|Per %1 non è disponibile una colonna di origine corrispondente nello schema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|La tabella, la vista o la colonna di riferimento utilizzata per i termini di riferimento non è valida.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|La tabella, la vista o la colonna di riferimento utilizzata per i termini di riferimento non è stata impostata.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|Esiste un mapping tra %1 e la colonna di metadati esterna con ID %2!ld!, di cui è già stato eseguito il mapping a un'altra colonna.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|Il nome di oggetto SQL '%1' specificato per la proprietà '%2' contiene un numero di prefissi superiore al massimo consentito.  di 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|Valore troppo grande per le dimensioni della colonna.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|L'interfaccia IDataReader SSIS è chiusa.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|L'interfaccia IDataReader SSIS è oltre la fine del risultato.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|La posizione ordinale della colonna non è valida.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|Impossibile convertire %1 dal tipo di dati "%2" al tipo di dati "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|Per %1 è impostata la tabella codici non supportata %2!d!.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|Per %1 non è stato definito un mapping a XML Schema.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Metadati non corrispondenti per le colonne con ID di derivazione %1!d! e %2!d! . La colonna di input di cui è stato eseguito il mapping a una colonna di output non dispone degli stessi metadati (tipo di dati, precisione, scala, lunghezza o tabella codici).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|L'interfaccia IDataReader SSIS è chiusa. Timeout di lettura scaduto.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|Errore durante l'esecuzione del comando SQL specificato: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|Il valore della proprietà JoinType specificato per la colonna di input '%1' è diverso dal valore JoinType specificato per la colonna della tabella di riferimento corrispondente al momento della creazione iniziale dell'indice delle corrispondenze.  Ricompilare l'indice delle corrispondenze con il valore JoinType indicato oppure modificare la proprietà JoinType in modo che il valore corrisponda al tipo utilizzato per la creazione iniziale dell'indice delle corrispondenze.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|Il tipo di dati "%1" rilevato nella colonna "%2" non è supportato per "%3".|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|Il tipo di dati "%1" rilevato in "%2" non è supportato per "%3".|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|Il tipo di dati di %1 non è supportato per %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Impossibile aggiungere un riferimento al progetto "%1" durante la migrazione di %2. Potrebbe essere necessario completare la migrazione manualmente.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Durante la migrazione di %2 sono stati trovati più punti di ingresso denominati "%1". Potrebbe essere necessario completare la migrazione manualmente.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|Durante la migrazione di %1 non è stato trovato alcun punto di ingresso. Potrebbe essere necessario completare la migrazione manualmente.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|Eccezione durante l'inserimento dei dati. Il messaggio restituito dal provider è: %1.|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Impossibile recuperare il nome invariante del provider da %1 poiché non è attualmente supportato dal componente di destinazione ADO.NET.|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|Eccezione relativa all'argomento durante il tentativo di inserimento dei dati nella destinazione. Il messaggio restituito è: %1.|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|Il valore della proprietà BatchSize deve essere un numero intero non negativo.|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|Errore durante l'invio della riga all'origine dati di destinazione.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|L'esecuzione del comando tSQL genera un'eccezione. Il messaggio restituito è: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|Il tipo di dati "%1" rilevato nella colonna "%2" non è supportato per "%3".|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|Il componente di destinazione ADO.NET non è in grado di acquisire la connessione %1. La connessione potrebbe essere danneggiata.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|La connessione specificata %1 non è gestita. Utilizzare una connessione gestita per la destinazione ADO.NET.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|Al componente di destinazione non è associato un output errori. Il componente potrebbe essere danneggiato.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|Il valore lineageID %1 associato alla colonna esterna %2 non esiste in fase di esecuzione.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|%1 non esiste nel database. Potrebbe essere stato spostato o rinominato.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Impossibile recuperare le proprietà delle colonne esterne. Il nome della tabella specificato non esiste o nell'oggetto tabella non è presente un'autorizzazione SELECT e non è stato possibile eseguire un tentativo di recuperare le proprietà della colonna mediante una connessione. I messaggi di errore dettagliati sono: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|La disposizione con errore per le colonne di input non è supportata dal componente di destinazione ADO.NET.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|La disposizione con troncamenti di input non è supportata dal componente di destinazione ADO.NET.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|La disposizione per le righe con troncamenti di input non è supportata dal componente di destinazione ADO.NET.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|Il nome tabella o vista non previsto. \n\t Se il nome della tabella deve essere racchiuso tra virgolette, utilizzare il prefisso %1 e il suffisso %2 del provider di dati selezionato. \n\t Se si utilizza un nome in più parti, utilizzarne almeno tre per il nome della tabella.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Impossibile trovare la colonna "%1" con ID di derivazione %2!d! nel buffer. Codice di errore restituito da Gestione buffer: 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Impossibile ottenere informazioni per la colonna "%1" (%2!d!) dal buffer. Codice di errore restituito: 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Overflow aritmetico durante l'aggregazione "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Impossibile ottenere informazioni per la riga %1!ld!, colonna %2!ld! dal buffer. Codice di errore restituito: 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Impossibile impostare le informazioni per la riga %1!ld!, colonna %2!ld! nel buffer. Codice di errore restituito: 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|Un buffer necessario non è disponibile.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|Tentativo di recupero delle informazioni sui limiti del buffer non riuscito con codice di errore: 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Impossibile impostare la fine del set di righe per il buffer. Codice di errore: 0x%1!8.8X!|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Impossibile ottenere dati per il buffer dell'output degli errori.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Impossibile rimuovere una riga dal buffer. Codice di errore: 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|Tentativo di impostazione delle informazioni sugli errori del buffer non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|Errore per %1 in %2. Stato della colonna restituito: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Impossibile memorizzare i metadati di riferimento nella cache.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|Nessuna corrispondenza per la riga durante la ricerca.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|Per %1 è impostata una disposizione non valida per le righe con errori o troncamenti.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Impossibile indirizzare la riga all'output degli errori. Codice di errore: 0x%1!8.8X!|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Impossibile preparare gli stati delle colonne per l'inserimento. Codice di errore: 0x%1!8.8X!|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|Impossibile trovare %1 con ID di derivazione %2!d! nel buffer dell'attività Flusso di dati. Codice di errore: 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Impossibile trovare colonne di errori non speciali in %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|Codice di errore SSIS DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  Errore di "%1" con codice 0x%2!8.8X!. La disposizione per le righe con errori in "%3" prevede l'interruzione in caso di errore. Si è verificato un errore nell'oggetto specificato del componente specificato.  Possono essere presenti ulteriori messaggi di errore prima di questo con informazioni aggiuntive sull'errore.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|Errore di "%1" a causa di un troncamento. La disposizione per le righe con troncamenti in "%2" prevede l'interruzione in caso di troncamento. Si è verificato un errore di troncamento nell'oggetto specificato del componente specificato.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|L'espressione "%1" in "%2" ha restituito NULL ma "%3" richiede risultati booleani. Modificare la disposizione per le righe con errori nell'output in modo da trattare questo risultato come False (Ignora errore) oppure per reindirizzare la riga all'output degli errori (Reindirizza riga).  I risultati dell'espressione devono essere booleani per una trasformazione Suddivisione condizionale.  Un'espressione NULL genera un errore.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|L'espressione ha restituito NULL ma richiede risultati booleani. Modificare la disposizione per le righe con errori nell'output in modo da trattare questo risultato come False (Ignora errore) oppure per reindirizzare la riga all'output degli errori (Reindirizza riga). I risultati dell'espressione devono essere booleani per una trasformazione Suddivisione condizionale.  Un'espressione NULL genera un errore.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|Formato di file UTF-16 big endian non supportato.  È supportato solo il formato UTF-16 little endian.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|Il formato di file UTF-8 non è supportato come Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Impossibile leggere l'attributo ID.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|Più colonne di input ricerca fanno riferimento alla colonna dell'indice della cache %1.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|La ricerca non fa riferimento a tutte le colonne dell'indice della gestione connessione della cache. Numero di colonne unite nella ricerca: %1!d!. Numero di colonne dell'indice: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|Impossibile convertire il valore di dati per motivi diversi dalla non corrispondenza di segno o dall'overflow dei dati.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|Il valore di dati viola il vincolo dello schema.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|Dati troncati.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Impossibile eseguire la conversione. Il valore di dati è con segno mentre il tipo utilizzato dal provider è senza segno.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Impossibile eseguire la conversione. Overflow del valore di dati rispetto al tipo utilizzato dal provider.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|Stato non disponibile.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|L'utente non dispone delle autorizzazioni corrette per la scrittura nella colonna.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|Il valore di dati viola i vincoli di integrità per la colonna.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|Stato non disponibile.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|Impossibile convertire il valore di dati per motivi diversi dalla non corrispondenza di segno o dall'overflow dei dati.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|Dati troncati.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Impossibile eseguire la conversione. Il valore di dati è con segno mentre il tipo utilizzato dal provider è senza segno.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Impossibile eseguire la conversione. Overflow del valore di dati rispetto al tipo utilizzato dal provider.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|Il valore di dati viola il vincolo dello schema.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|Impossibile convertire il valore di dati per motivi diversi dalla non corrispondenza di segno o dall'overflow dei dati.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|Dati troncati.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Impossibile eseguire la conversione. Il valore di dati è con segno mentre il tipo utilizzato dal provider è senza segno.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Impossibile eseguire la conversione. Overflow del valore di dati rispetto al tipo utilizzato dal provider.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|Stato non disponibile.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|L'utente non dispone delle autorizzazioni corrette per la scrittura nella colonna.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|Il valore di dati viola i vincoli di integrità.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|Impossibile convertire il valore di dati per motivi diversi dalla non corrispondenza di segno o dall'overflow dei dati.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|Dati troncati.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Impossibile eseguire la conversione. Il valore di dati è con segno mentre il tipo utilizzato dal provider è senza segno.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Impossibile eseguire la conversione. Overflow del valore di dati rispetto al tipo utilizzato dalla trasformazione per la conversione dei dati.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|Stato non disponibile.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|Impossibile convertire il valore di dati per motivi diversi dalla non corrispondenza di segno o dall'overflow dei dati.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|Dati troncati.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Impossibile eseguire la conversione. Il valore di dati è con segno mentre il tipo utilizzato dall'adattatore di origine file flat è senza segno.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Impossibile eseguire la conversione. Overflow del valore di dati rispetto al tipo utilizzato dall'adattatore di origine file flat.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|Stato non disponibile.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Impossibile aprire il file "%1" per la lettura. Codice di errore: 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Impossibile aprire il file per la lettura.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Impossibile aprire il file "%1" per la scrittura. Codice di errore: 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Impossibile aprire il file per la scrittura.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Impossibile leggere dal file.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Impossibile scrivere nel file.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Troppi elementi di matrice trovati durante l'analisi di una proprietà di tipo matrice. Il valore elementCount è inferiore al numero di elementi della matrice trovati.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Numero insufficiente di elementi di matrice trovati durante l'analisi di una proprietà di tipo matrice. Il valore elementCount è maggiore del numero di elementi della matrice trovati.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Impossibile aprire il file "%1" per la scrittura. Impossibile trovare il file.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Impossibile aprire il file per la scrittura. Impossibile trovare il file.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Impossibile aprire il file "%1" per la scrittura. Impossibile trovare il percorso.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Impossibile aprire il file per la scrittura. Impossibile trovare il percorso.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Impossibile aprire il file "%1" per la scrittura. Troppi file aperti.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Impossibile aprire il file per la scrittura. Troppi file aperti.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Impossibile aprire il file "%1" per la scrittura. Non sono disponibili le autorizzazioni corrette.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Impossibile aprire il file per la scrittura. Non sono disponibili le autorizzazioni corrette.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Impossibile aprire il file "%1" per la scrittura. Il file esiste e non può essere sovrascritto. Se la proprietà AllowAppend è impostata su FALSE e la proprietà ForceTruncate è impostata su FALSE, l'esistenza del file causa questo errore.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Impossibile aprire il file per la scrittura. Il file esiste già e non può essere sovrascritto. Se sia la proprietà AllowAppend che la proprietà ForceTruncate sono impostate su FALSE, l'esistenza del file causa questo errore.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|Il valore per la proprietà personalizzata "%1" in %2 non è corretto.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Metadati non compatibili per le colonne "%1" e "%2".|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Impossibile aprire il file "%1" per la scrittura perché il disco è pieno. Spazio su disco insufficiente per salvare il file.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Impossibile aprire il file per la scrittura perché il disco è pieno.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Impossibile generare una chiave di ordinamento. Errore: 0x%1!8.8X!. I flag ComparisonFlags sono abilitati e non è possibile generare una chiave di ordinamento con LCMapString.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|La trasformazione non è riuscita a eseguire il mapping di una stringa. Errore restituito: 0x%1!8.8X!. Operazione LCMapString non riuscita.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Impossibile aprire il file "%1" per la lettura. Impossibile trovare il file.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Impossibile aprire un file per la lettura. Impossibile trovare il file.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Impossibile aprire il file "%1" per la lettura. Impossibile trovare il percorso.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Impossibile aprire un file per la lettura. Impossibile trovare il percorso.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Impossibile aprire il file "%1" per la lettura. Troppi file aperti.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Impossibile aprire il file per la lettura. Troppi file aperti.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Impossibile aprire il file "%1" per la lettura. Accesso negato.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Impossibile aprire il file per la lettura. Non sono disponibili le autorizzazioni corrette.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|Il valore dell'indicatore per l'ordine dei byte (BOM) per il file "%1" è 0x%2!4.4X!, ma il valore previsto è 0x%3!4.4X!. Per il file è stata impostata la proprietà ExpectBOM, ma il valore BOM non è disponibile nel file o non è valido.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|Il valore dell'indicatore per l'ordine dei byte (BOM) per il file non è valido. Per il file è stata impostata la proprietà ExpectBOM, ma il valore BOM non è disponibile nel file o non è valido.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1 non è collegato a un componente.  È necessario collegare un componente.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|Il valore per la proprietà personalizzata %1 non è corretto.  Deve essere un numero compreso nell'intervallo da %2!d! a %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|Impossibile specificare la proprietà personalizzata "%1" per il tipo di aggregazione selezionato per la colonna. La proprietà personalizzata per i flag di confronto può essere specificata solo per i tipi di aggregazione Group By e Count Distinct.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|La proprietà personalizzata per i flag di confronto "%1" può essere specificata solo per le colonne con tipo di dati DT_STR o DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Impossibile eseguire l'aggregazione su %1. Codice di errore: 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|Errore durante l'impostazione del mapping. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1 non ha potuto leggere i dati XML.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1 non ha potuto recuperare la variabile specificata dalla proprietà "%2".|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1 contiene un RowsetID con il valore %2 che non fa riferimento a una tabella di dati nello schema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|La proprietà %1 deve essere vuota o un numero compreso tra %2!u! e %3!u!. Il valore della proprietà Keys o CountDistinctKeys non è valido. Il valore della proprietà deve essere un numero compreso tra 0 e ULONG_MAX, inclusi, oppure la proprietà non deve essere impostata.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|Il componente di aggregazione ha rilevato troppe combinazioni di chiavi distinct e non supporta più di %1!u! valori di chiave distinct. L'area di lavoro principale include più valori di chiave distinct di quanto consentito da ULONG_MAX.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|Il componente di aggregazione ha rilevato troppi valori distinct durante il calcolo dell'aggregazione Count Distinct. e non supporta più di %1!u! valori distinct. Durante il calcolo dell'aggregazione Count Distinct sono stati rilevati più valori distinct di quanto consentito da ULONG_MAX.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|Tentativo di scrittura nella colonna del nome di file non riuscito con codice di errore 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|Si è verificato un errore ma non è possibile determinare la colonna che ha causato l'errore.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Impossibile aggiornare i metadati di ricerca dalla versione %1!d! a %2!d!. La trasformazione Ricerca non ha potuto aggiornare i metadati dal numero di versione esistente in una chiamata a PerformUpgrade().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Impossibile individuare il limite finale di una frase.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|La trasformazione Estrazione termini non è in grado di elaborare il testo di input perché una frase presente nel testo di input è troppo lunga. La frase è segmentata in più frasi.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1 non ha potuto leggere i dati XML. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|Chiamata non riuscita al metodo ReinitializeMetadata della trasformazione Ricerca.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|La trasformazione Ricerca deve includere almeno una colonna di input unita in join a una colonna di riferimento. Nessuna colonna specificata. È necessario specificare almeno una colonna di join.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|La stringa di messaggio inviata dall'infrastruttura dell'errore gestito contiene una specifica di formato non valida. Errore interno.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|Durante la formattazione di una stringa di messaggio tramite l'infrastruttura dell'errore gestito è stato rilevato un tipo variant per cui non è disponibile il supporto per la formattazione. Errore interno.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1 non ha potuto elaborare i dati. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|La proprietà "%1" in %2 è vuota.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Impossibile creare un output con il nome "%1" per la tabella XML con il percorso "%2". Nome non valido.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|Valore troppo grande per le dimensioni della colonna %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1 non ha potuto elaborare i dati.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|Errore di "%1" a causa di un troncamento. La disposizione per le righe con troncamenti in "%2" in "%3" prevede l'interruzione in caso di troncamento. Si è verificato un errore di troncamento nell'oggetto specificato del componente specificato.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|Errore di "%1" con codice 0x%2!8.8X!. La disposizione per le righe con errori in "%3" in "%4" prevede l'interruzione in caso di errore. Si è verificato un errore nell'oggetto specificato del componente specificato.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|La destinazione SQLCE non ha potuto impostare i valori di colonna per la riga.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|La destinazione di SQLCE non ha potuto inserire la riga.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Errore OLE DB durante il caricamento dei metadati della colonna.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Numero di colonne insufficiente nei metadati di riferimento per la trasformazione Ricerca.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Errore OLE DB durante il caricamento dei metadati della colonna.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Numero di colonne insufficiente nei metadati di riferimento per la trasformazione Ricerca.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Impossibile allocare memoria.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Impossibile allocare memoria.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Impossibile creare il buffer per l'area di lavoro.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Impossibile creare un'istanza del documento DOM XML. Verificare che i file binari MSXML siano installati e registrati correttamente.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|Impossibile caricare i dati XML in un documento DOM locale per l'elaborazione.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|Il tipo della variabile di run-time "%1" non è corretto. La variabile di run-time deve essere di tipo Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|L'adattatore di origine XML non ha potuto elaborare i dati. Non sono supportati più schemi inline.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|L'adattatore di origine XML non ha potuto elaborare i dati. Impossibile dichiarare il contenuto di un elemento come anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|L'adattatore di origine XML non ha potuto elaborare i dati. Il contenuto di un elemento non può contenere un riferimento (ref) a un gruppo.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|L'adattatore di origine XML non supporta il modello di contenuto misto per i tipi complessi.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|L'adattatore di origine XML non ha potuto elaborare i dati. Uno schema inline deve essere il primo nodo figlio nel codice XML di origine.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|L'adattatore di origine XML non ha potuto elaborare i dati. Impossibile trovare uno schema inline nel codice XML di origine, ma la proprietà "UseInlineSchema" è impostata su true.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|Il componente non può utilizzare una gestione connessione che mantiene la connessione in una transazione con caricamento rapido o inserimento bulk.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|%1 non è in grado di impostare il reindirizzamento in caso di errore utilizzando una connessione in una transazione.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|Per %1 non è disponibile una colonna di input o output corrispondente.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|Nessuna colonna selezionata per la scrittura nel file.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|Il tipo di dati %1 non è valido. Impossibile scrivere colonne con tipo di dati DT_IMAGE, DT_TEXT e DT_NTEXT nei file non elaborati.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|Utilizzo non appropriato della raccolta dei metadati esterni nel componente. I metadati esterni dovrebbero essere utilizzati per l'accodamento o il troncamento di un file esistente. Negli altri casi, i metadati esterni non sono necessari.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|Esiste un mapping tra %1 e la colonna di metadati esterna con ID %2!d!. Il mapping delle colonne di input a colonne di metadati esterne non dovrebbe essere eseguito quando il valore selezionato per la proprietà WriteOption è Crea sempre.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|Impossibile aprire il file per la lettura dei metadati. Se il file non esiste e il componente ha già definito i metadati esterni, è possibile impostare la proprietà "ValidateExternalMetadata" su "false" in modo che il file venga creato in fase di esecuzione.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Impossibile accedere ai dati LOB dal buffer del flusso di dati per la colonna di origine dei dati "%1". Codice di errore: 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1 non ha potuto elaborare i dati XML. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|L'adattatore di origine XML non ha potuto elaborare i dati.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|Il valore %1!d! non è riconosciuto come modalità di accesso valida.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Non sono disponibili informazioni complete sui metadati per la colonna dell'origine dei dati "%1".  Verificare che la colonna sia definita in modo corretto nell'origine dei dati.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|È possibile modificare solo la lunghezza di una colonna relativa al nome utente, al nome pacchetto, al nome attività e al nome computer.  Tutte le altre informazioni sui tipi di dati delle colonne di controllo sono di sola lettura.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|Il provider OLE DB non ha restituito un set di righe basato sul comando SQL.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|Commit non riuscito.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|La proprietà personalizzata "%1" di %2 può essere utilizzata solo con file ANSI.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|La proprietà personalizzata "%1" di %2 può essere utilizzata solo con DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|Codice di errore SSIS DTS_E_OLEDB_NOPROVIDER_ERROR.  Il provider OLE DB %2 necessario non è registrato. Codice errore: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|Codice di errore SSIS DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  Il provider OLE DB %2 necessario non è registrato. È possibile che non siano disponibili provider a 64 bit.  Codice errore: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|È stato eseguito il mapping della colonna della cache "%1" a più colonne. Rimuovere i mapping duplicati della colonna.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|Non è stato eseguito il mapping di %1 a una colonna della cache valida.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Impossibile eseguire il mapping della colonna di input "%1" e della colonna della cache "%2" perché i tipi di dati non corrispondono.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|Il numero di colonne di input non corrisponde al numero di colonne della cache.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|Il nome del file di cache non è stato fornito o non è valido. Fornire un nome di file di cache valido.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|La posizione dell'indice della colonna "%1" è diversa dalla posizione dell'indice della colonna della gestione connessione della cache "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Impossibile caricare la cache dal file "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|La colonna di input ricerca %1 fa riferimento alla colonna della cache non di indice %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Impossibile ottenere la stringa di connessione.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Impossibile eseguire il mapping della colonna di input "%1" e della colonna della cache "%2" perché una o più proprietà del tipo di dati non corrispondono.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Impossibile trovare la colonna della cache "%1" nella cache.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Impossibile eseguire il mapping di %1 a una colonna della cache. Hresult: 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|%1 non è in grado di scrivere nella cache perché la cache è stata caricata da un file da %2.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|%1 non è in grado di caricare la cache dal file "%2" perché la cache è già stata caricata dal file "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|L'output con ID %1!d! del componente di aggregazione non è in uso da parte di alcun componente. Rimuoverlo o associarlo all'input di qualche componente.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 non è riuscito a scrivere la cache nel file "%2". Hresult: 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|Le informazioni sul tipo di dati di XML Schema per "%1" nell'elemento "%2" sono state modificate.  Reinizializzare i metadati per questo componente e verificare i mapping delle colonne.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 non utilizzato in operazioni di join o di copia. Rimuovere la colonna inutilizzata dall'elenco delle colonne di input.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|Ordinamento non riuscito a causa di un overflow dello stack durante l'ordinamento di un buffer in ingresso.  Ridurre la proprietà DefaultBufferMaxRows nell'attività Flusso di dati.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Provare a cambiare il PROVIDER nella stringa di connessione in %1 oppure visitare https://www.microsoft.com/downloads per individuare e installare il supporto per %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Impossibile inizializzare l'oggetto attività per l'attività "%1!s!", tipo "%2!s!" a causa dell'errore 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Impossibile creare il responsabile delle categorie componenti COM a causa dell'errore 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|Impossibile inizializzare il componente %1!s! a causa dell'errore 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Messaggi di avviso  
 I nomi simbolici dei messaggi di avviso di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] iniziano con **DTS_W_** .  
  
|Codice esadecimale|Codice decimale|Nome simbolico|Descrizione|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|Il periodo di valutazione scade fra %1!lu! giorni. Dopo la scadenza non sarà più possibile eseguire i pacchetti.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Sono stati generati uno o più avvisi. Prima di questo avviso dovrebbero essere presenti altri avvisi più specifici con spiegazioni dettagliate.|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Impossibile creare un'istanza dell'oggetto documento XML. Verificare che MSXML sia installato e registrato correttamente.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Impossibile caricare il file di configurazione XML. È possibile che sia in formato non corretto o che non sia valido.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|Il nome del file di configurazione "%1" non è valido. Controllare il nome del file di configurazione.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|Il file di configurazione è stato caricato ma non è valido. Il formato del file non è corretto, manca un elemento oppure il file è danneggiato.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|Impossibile trovare il file di configurazione "%1". Controllare la directory e il nome del file.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Impossibile trovare la chiave del Registro di sistema "%1" della configurazione. Una voce di configurazione specifica una chiave del Registro di sistema non disponibile. Controllare il Registro di sistema per assicurarsi che la chiave sia presente.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|Il tipo di configurazione in una delle voci di configurazione non è valido. I tipi validi sono elencati nell'enumerazione DTSConfigurationType.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|Il percorso del pacchetto fa riferimento a un oggetto non trovato: "%1". Questo errore si verifica quando si tenta di risolvere il percorso di un pacchetto su un oggetto non disponibile.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|Il formato della voce di configurazione "%1" non è corretto. Non inizia con il delimitatore di pacchetto. Anteporre "\package" al percorso del pacchetto.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|Il formato della voce di configurazione "%1" non è corretto. Il problema può essere causato da un delimitatore mancante o da errori di formattazione, come un delimitatore di matrice non valido.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|Impossibile eseguire la configurazione da una variabile padre "%1" perché non è disponibile la raccolta della variabile padre.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Errore durante l'importazione dei file di configurazione: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|Impossibile eseguire la configurazione da una variabile padre "%1" perché la variabile padre non è disponibile. Codice errore: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|Il file di configurazione è vuoto e non contiene voci di configurazione.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|Il tipo di configurazione per la configurazione "%1" non è valido. La causa dell'errore potrebbe essere il tentativo di impostare la proprietà del tipo di un oggetto di configurazione su un tipo di configurazione non valido.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|Impossibile trovare il tipo di configurazione per la configurazione del Registro di sistema nella chiave "%1". Aggiungere un valore denominato ConfigType alla chiave del Registro di sistema e assegnare un valore stringa "Variable", "Property", "ConnectionManager", "LoggingProvider" o "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|Impossibile trovare il valore di configurazione per la configurazione del Registro di sistema nella chiave "%1". Aggiungere un valore denominato Value alla chiave del Registro di sistema con tipo DWORD o String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Impossibile impostare la destinazione nel percorso del pacchetto "%1" tramite la configurazione del processo. Questo errore si verifica quando il tentativo di impostare la variabile o la proprietà di destinazione non riesce. Controllare la proprietà o la variabile di destinazione.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Impossibile recuperare il valore dal file INI. La sezione ConfiguredValue è vuota o non esiste: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Impossibile recuperare il valore dal file INI. La sezione ConfiguredType è vuota o non esiste: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Impossibile recuperare il valore dal file INI. La sezione PackagePath è vuota o non esiste: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Impossibile recuperare il valore dal file INI. La sezione ConfiguredValueType è vuota o non esiste: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|Impossibile completare l'importazione della configurazione da SQL Server: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|Il file di configurazione INI non è valido a causa di campi vuoti o mancanti.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|La tabella "%1" non include alcun record per la configurazione. Questo errore si verifica quando si tenta di configurare una tabella di SQL Server che non contiene record per la configurazione.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Errore durante l'utilizzo dello stesso nome per eventi personalizzati diversi. L'evento personalizzato "%1" è stato definito in modo diverso da figli differenti di questo contenitore. È possibile che si verifichi un errore durante l'esecuzione del gestore dell'evento.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|La configurazione ha eseguito un tentativo di modifica di una variabile di sola lettura. La variabile si trova nel percorso del pacchetto "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Impossibile chiamare ProcessConfiguration sul pacchetto. La configurazione ha eseguito un tentativo di modifica della proprietà nel percorso del pacchetto "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Impossibile caricare almeno una voce di configurazione per il pacchetto. Controllare le voci di configurazione per "%1" e gli avvisi precedenti per visualizzare le descrizioni delle voci di configurazione con problemi.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|La voce di configurazione "%1" nel file di configurazione non è valida o non è riuscita a configurare la variabile.  Il nome indica la voce in errore. In alcuni casi, il nome non sarà disponibile.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|Errore dell'attività o del contenitore. Poiché la proprietà FailPackageOnFailure è FALSE, l'esecuzione del pacchetto continuerà. Questo avviso viene generato quando la proprietà SaveCheckpoints del pacchetto è impostata su TRUE e si verifica un errore a livello dell'attività o del contenitore.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|Il percorso è vuoto.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|Codice di avviso SSIS DTS_W_MAXIMUMERRORCOUNTREACHED.  Il metodo Execution è stato completato, ma il numero di errori generati (%1!d!) è pari al massimo consentito (%2!d!) e pertanto viene restituito un errore. Questo errore si verifica quando il numero di errori raggiunge il valore specificato in MaximumErrorCount. Modificare l'impostazione MaximumErrorCount o correggere gli errori.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|Impossibile trovare la variabile di ambiente di configurazione  "%1". Questo errore si verifica quando un pacchetto specifica una variabile di ambiente per un'impostazione di configurazione, ma non è possibile trovare la variabile. Controllare la raccolta delle configurazioni nel pacchetto e verificare che la variabile di ambiente specificata sia disponibile e valida.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|Il nome del provider della gestione connessione "%1" è stato cambiato da "%2" a "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|Eccezione durante la lettura dei file di mapping dell'aggiornamento. Eccezione: "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|Mapping duplicato nel file "%1". Tag "%2", chiave "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|Estensione "%1" aggiornata in modo implicito in "%2". Aggiungere un mapping per questa estensione alla directory UpgradeMappings.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|Un mapping nel file "%1" non è valido. I valori non possono essere Null o vuoti. Tag "%2", chiave "%3", valore "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|La proprietà DataTypeCompatibility della gestione connessione di tipo ADO "%1" è stata impostata su 80 per motivi di compatibilità con le versioni precedenti.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|L'enumeratore For Each File è vuoto. Impossibile trovare file corrispondenti ai criteri impostati oppure la directory specificata è vuota.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Impossibile risolvere un percorso di pacchetto in un oggetto nel pacchetto "%1". Controllare che il percorso del pacchetto sia valido.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|L'espressione di iterazione non è di assegnazione: "%1". Questo errore si verifica in genere quando l'espressione nell'espressione di assegnazione in ForLoop non è di assegnazione.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|L'espressione di inizializzazione non è di assegnazione: "%1". Questo errore si verifica in genere quando l'espressione nelle espressioni di iterazione in ForLoop non è di assegnazione.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|Copia del file eseguibile "%1" completata. Tuttavia, un provider di log associato al file eseguibile non è stato trovato nella raccolta "LogProvider".  Il file eseguibile è stato copiato senza le informazioni sul provider di log.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Aggiornamento del pacchetto completato.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|Il ProgID "%1" è stato dichiarato deprecato. Utilizzare pertanto il nuovo ProgID per questo componente "%2".|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Operazione "%1" non riuscita.|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|Nell'algoritmo di crittografia "%1" viene utilizzata la crittografia vulnerabile.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Impossibile eseguire l'operazione "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|Impossibile trovare il file/processo "%1" nel percorso.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|L'oggetto è vuoto.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|Il formato dell'indirizzo nella riga "A" non è corretto. Non è valido o manca il simbolo "\@".|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|Il formato dell'indirizzo nella riga "Da" non è corretto. Non è valido o manca il simbolo "\@".|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|I due documenti XML sono diversi.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|La convalida DTD utilizzerà il file DTD definito nella riga DOCTYPE del documento XML anziché il valore assegnato alla proprietà "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Impossibile convalidare "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|Il valore dell'azione di trasferimento non è valido.  Verrà impostato sulla copia.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|Il valore del metodo di trasferimento non è valido.  Verrà impostato sul trasferimento online.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|Problema con i messaggi seguenti: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|Il messaggio di errore "%1" esiste già nel server di destinazione.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|Il processo "%1" esiste già nel server di destinazione.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Il processo "%1" non verrà trasferito perché esiste già nella destinazione.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Sovrascrittura del processo "%1" nel server di destinazione in corso.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Il valore di enumerazione persistente della proprietà "FailIfExists" è stato modificato e non è più valido. Reimpostazione del valore predefinito in corso.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Sovrascrittura dell'account di accesso "%1" nella destinazione in corso.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|La stored procedure "%1" esiste già nella destinazione.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|La regola "%1" esiste già nella destinazione.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|La tabella "%1" esiste già nella destinazione.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|La vista "%1" esiste già nella destinazione.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|La funzione definita dall'utente "%1" esiste già nella destinazione.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Il valore predefinito "%1" esiste già nella destinazione.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|Il tipo di dati definito dall'utente "%1" esiste già nella destinazione.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|La funzione di partizione "%1" esiste già nella destinazione.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|Lo schema di partizione "%1" esiste già nella destinazione.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Lo schema "%1" esiste già nella destinazione.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|L'assembly SQL "%1" esiste già nella destinazione.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|La funzione di aggregazione definita dall'utente "%1" esiste già nella destinazione.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|Il tipo definito dall'utente (UDT) "%1" esiste già nella destinazione.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|La raccolta di schemi XML "%1" esiste già nella destinazione.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|Nessun elemento specificato per il trasferimento.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|L'account di accesso "%1" esiste già nella destinazione.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|L'utente "%1" esiste già nella destinazione.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|Impossibile convalidare gli ID di derivazione delle colonne di input perché sono presenti cicli negli alberi di esecuzione.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|Nessun componente nell'attività DataFlow. Aggiungere componenti o rimuovere l'attività.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|La proprietà IsSorted di %1 è impostata su TRUE, ma la proprietà SortKeyPosition per tutte le colonne di output corrispondenti è impostata su zero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|L'origine "%1" (%2!d!) non verrà letta perché i relativi dati non saranno mai visibili all'esterno dell'attività Flusso di dati.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|La colonna di output "%1" (%2!d!) nell'output "%3" (%4!d!) e nel componente "%5" (%6!d!) non verrà più utilizzata nell'attività Flusso di dati. La rimozione di questa colonna di output inutilizzata può migliorare le prestazioni dell'attività Flusso di dati.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Il componente "%1" (%2!d!) è stato rimosso dall'attività Flusso di dati poiché l'output non viene utilizzato e gli input non hanno effetti collaterali o non sono connessi agli output di altri componenti. Se il componente è necessario, impostare la proprietà HasSideEffects in almeno uno degli input su true o connettere l'output.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Sono state passate righe a un thread, ma il thread non deve eseguire alcuna operazione. Il layout include un output disconnesso. Se si esegue la pipeline con la proprietà RunInOptimizedMode impostata su TRUE, questa sarà più veloce e si eviterà questo avviso.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|Le colonne esterne per %1 non sono sincronizzate con le colonne dell'origine dati. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|È necessario aggiungere la colonna "%1" alle colonne esterne.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|È necessario aggiornare la colonna esterna "%1".|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|È necessario rimuovere %1 dalle colonne esterne.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|È possibile che la stringa di risultato per l'espressione "%1" venga troncata se supera la lunghezza massima di %2!d! caratteri. L'espressione potrebbe restituire un valore di dimensioni superiori al massimo consentito per un tipo DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|Una chiamata al metodo ProcessInput per l'input %1!d! in %2 ha mantenuto un riferimento al buffer passato, in modo imprevisto. Il conteggio dei riferimenti nel buffer era %3!d! prima della chiamata e %4!d! dopo il completamento della chiamata.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|Per "%1" in "%2" è impostato il tipo di utilizzo READONLY, ma non esiste un riferimento a tale colonna da un'espressione. Rimuovere la colonna dall'elenco delle colonne di input disponibili oppure aggiungere un riferimento alla colonna in un'espressione.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Impossibile trovare il valore "%1" per il componente %2. Impossibile trovare il valore CurrentVersion per il componente. Questo errore si verifica se le informazioni del Registro di sistema impostate per il componente non includono un valore CurrentVersion nella sezione DTSInfo. Questo messaggio viene generato durante lo sviluppo del componente oppure quando si utilizza il componente in un pacchetto se il componente non è registrato in modo appropriato.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|Gestione buffer non ha potuto ottenere un nome di file temporaneo.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|Gestione buffer non ha potuto creare un file temporaneo nel percorso "%1". Il percorso non verrà ripreso in considerazione per l'archiviazione temporanea.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Avviso: impossibile aprire la memoria condivisa globale per comunicare con la DLL di prestazioni; i contatori di prestazioni del flusso di dati non sono disponibili.  Per risolvere il problema, eseguire questo pacchetto con privilegi di amministratore o sulla console di sistema.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|Riga parziale alla fine del file.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|È stata raggiunta la fine del file di dati durante la lettura delle righe di intestazione. Verificare che il delimitatore delle righe di intestazione e il numero di righe di intestazione da ignorare siano corretti.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Impossibile recuperare le informazioni sulla tabella codici della colonna dal provider OLE DB.  Se il componente supporta la proprietà "%1", verrà utilizzata la tabella codici da tale proprietà.  Modificare il valore della proprietà se i valori della tabella codici per la stringa corrente non sono corretti.  Se il componente non supporta la proprietà, verrà utilizzata la tabella codici dall'ID impostazioni locali del componente.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|I dati sono già nell'ordine specificato, quindi la trasformazione può essere rimossa.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 fa riferimento a un tipo di dati esterno di cui non è possibile eseguire il mapping a un tipo di dati dell'attività Flusso di dati. In alternativa, verrà utilizzato il tipo di dati DT_WSTR dell'attività Flusso di dati.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|L'espressione "%1" causerà sempre un troncamento dei dati. L'espressione contiene un troncamento statico (troncamento di un valore fisso).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|Nessun mapping definito per la colonna di input "%1" con ID %2!d! in corrispondenza dell'indice %3!d! . L'ID di derivazione per la colonna è zero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|I delimitatori specificati non corrispondono ai delimitatori utilizzati per compilare l'indice delle corrispondenze pre-esistente "%1". Questo errore si verifica quando i delimitatori utilizzati per suddividere i campi in token non corrispondono. L'errore può avere effetti sconosciuti sulla funzionalità di individuazione delle corrispondenze o sui risultati.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|La proprietà MaxOutputMatchesPerInput nella trasformazione Ricerca fuzzy è zero. Non verrà prodotto alcun risultato.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|Nessuna colonna di input valida con la proprietà JoinType impostata su Fuzzy.  È possibile migliorare le prestazioni dei join esatti utilizzando la trasformazione Ricerca anziché la trasformazione Ricerca fuzzy.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|La colonna di riferimento "%1" potrebbe essere una colonna timestamp SQL. Quando viene compilato l'indice delle corrispondenze fuzzy e creata una copia della tabella di riferimento, tutti i timestamp della tabella di riferimento rispecchieranno lo stato corrente della tabella al momento della copia. Se la proprietà CopyReferenceTable è impostata su False possono verificarsi risultati imprevisti.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|Esiste già una tabella con il nome '%1' specificato per MatchIndexName e la proprietà DropExistingMatchIndex è impostata su FALSE.  L'esecuzione della trasformazione avrà esito negativo a meno che la tabella non venga rimossa, non venga specificato un nome diverso o la proprietà DropExisitingMatchIndex non venga impostata su TRUE.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|La lunghezza della colonna di input '%1' non corrisponde alla lunghezza della colonna di riferimento '%2' con cui viene confrontata.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|Le tabelle codici della colonna di origine DT_STR "%1" e della colonna di destinazione DT_STR "%2" non corrispondono.  Si potrebbero verificare risultati imprevisti.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|Esistono più di 16 join di corrispondenza esatta, quindi le prestazioni potrebbero non essere ottimali. Ridurre il numero di join di corrispondenza esatta per migliorare le prestazioni. In SQL Server è previsto un limite di 16 colonne per indice e l'indice invertito verrà utilizzato per tutte le ricerche.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|Per l'opzione Exhaustive è necessario caricare l'intera tabella di riferimento nella memoria principale.  Poiché è stato impostato un limite di memoria per la proprietà MaxMemoryUsage, è possibile che l'intera tabella di riferimento non rientri in questo limite e che l'operazione di individuazione delle corrispondenze venga interrotta in fase di esecuzione.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|La lunghezza complessiva delle colonne specificate nei join di corrispondenza esatta supera il limite di 900 byte per le chiavi di indice.  La trasformazione Ricerca fuzzy crea un indice sulle colonne con corrispondenze esatte per migliorare le prestazioni della ricerca ed è possibile che la creazione di tale indice abbia esito negativo. In questo caso la ricerca verrà eseguita utilizzando un metodo alternativo, probabilmente più lento, per la ricerca delle corrispondenze. Se le prestazioni rappresentano un fattore significativo, provare a rimuovere alcune delle colonne di join di corrispondenza esatta oppure ridurre la lunghezza massima delle colonne di corrispondenze esatte a lunghezza variabile.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Impossibile creare un indice per le colonne di corrispondenze esatte. Verrà utilizzato un metodo alternativo di ricerca fuzzy.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|È stato generato l'avviso seguente della pipeline interna di raggruppamento fuzzy con il codice di avviso 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|Lunghezza massima non specificata per %1 con tipo di dati esterno %2. Verrà usato il tipo di dati "%3" dell'attività Flusso di dati SSIS con una lunghezza di %4!d! .|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1 fa riferimento al tipo di dati esterno %2 di cui non è possibile eseguire il mapping a un tipo di dati dell'attività Flusso di dati SSIS.  In alternativa, verrà utilizzato il tipo di dati DT_WSTR dell'attività Flusso di dati SSIS con una lunghezza di %3!d! .|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|Nessuna riga verrà inviata agli output degli errori. Configurare le disposizioni per gli errori o i troncamenti in modo che le righe vengano reindirizzate agli output degli errori oppure eliminare le trasformazioni o le destinazioni del flusso di dati collegate agli output degli errori.|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|Le righe inviate agli output degli errori andranno perdute. Aggiungere nuove trasformazioni o destinazioni del flusso di dati per la ricezione delle righe con errori oppure riconfigurare il componente in modo da arrestare il reindirizzamento delle righe agli output degli errori.|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|Per il %1 con tipo di dati esterno %2 in XML Schema è specificato un vincolo maxLength con valore %3!d!, che supera la lunghezza massima consentita per le colonne, pari a %4!d!. Verrà utilizzato il tipo di dati "%5" dell'attività Flusso di dati SSIS con una lunghezza di %6!d! .|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|%1 ha rilevato valori di chiave di riferimento duplicati durante la memorizzazione nella cache dei dati di riferimento. Questo errore si verifica solo in modalità di cache FULL. Rimuovere i valori di chiave duplicati oppure impostare la modalità di cache su PARTIAL o NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Potrebbero verificarsi errori di troncamento in seguito all'inserimento di dati dalla colonna del flusso di dati "%1" con lunghezza di %2!d! nella colonna del database "%3" con lunghezza di %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Potrebbero verificarsi errori di troncamento in seguito al recupero di dati dalla colonna del database "%1" con lunghezza di %2!d! nella colonna del flusso di dati "%3" con lunghezza di %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|La modalità batch non è attualmente supportata se viene utilizzata la disposizione di righe con errori. La proprietà BatchSize verrà impostata su 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|Nessuna riga inserita nella destinazione. I tipi potrebbero non corrispondere o potrebbe essere stato utilizzato un tipo di dati non supportato dal provider ADO.NET. Poiché la configurazione degli errori per questo componente non è del tipo "Interrompi componente", i messaggi di errore non verranno visualizzati. Per visualizzare i messaggi di errore, fare clic su "Interrompi componente".|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Perdita di dati potenziale a causa dell'inserimento di dati dalla colonna di input "%1" con tipo di dati "%2" nella colonna esterna "%3" con tipo di dati "%4". Se si desidera eseguire l'operazione, è possibile effettuare la conversione in modo alternativo utilizzando un componente per la conversione dei dati prima del componente di destinazione ADO.NET.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1 non è sincronizzato con la colonna di database.  La colonna più recente ha %2. Se necessario, utilizzare l'editor avanzato per aggiornare le colonne di destinazione.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|%1 non esiste nel database. Potrebbe essere stato spostato o rinominato. Se necessario, utilizzare l'editor avanzato per aggiornare le colonne di destinazione.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|Una nuova colonna denominata %1 è stata aggiunta alla tabella di database esterna. Se necessario, utilizzare l'editor avanzato per aggiornare le colonne di destinazione.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|Nessuna riga verrà inviata all'output nessuna corrispondenza. Configurare la trasformazione per reindirizzare le righe senza voci corrispondenti all'output nessuna corrispondenza oppure eliminare le trasformazioni del flusso di dati o le destinazioni collegate all'output nessuna corrispondenza.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Eccezione durante l'enumerazione dei provider ADO.NET. Invariante: "%1." Messaggio eccezione: %2.|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|Non è stato eseguito il mapping di nessuna colonna di input a %1.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|La tabella "%1" è stata modificata. È possibile che siano state aggiunte nuove colonne.|  
  
##  <a name="msgInfo"></a> Messaggi informativi  
 I nomi simbolici dei messaggi informativi di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] iniziano con **DTS_I_** .  
  
|Codice esadecimale|Codice decimale|Nome simbolico|Descrizione|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Avvio della transazione distribuita per questo contenitore in corso.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Commit della transazione distribuita avviata dal contenitore in corso.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Interruzione della transazione distribuita corrente in corso.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Acquisizione di mutex "%1" completata.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Rilascio di mutex "%1" completato.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Creazione di mutex "%1" completata.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|I file di dump del debug verranno generati per qualsiasi evento di errore.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|I file di dump del debug verranno generati per i seguenti codici evento: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Il codice evento 0x%1!8.8X! ha attivato la generazione dei file di dump del debug nella cartella "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Creazione del file di dump delle informazioni SSIS "%1" in corso.|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|File di dump del debug creati.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|Migrazione del formato del pacchetto dalla versione %1!d! alla versione %2!d!. È necessario salvare il pacchetto per mantenere le modifiche apportate durante la migrazione.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|Migrazione degli script del pacchetto completata. Per mantenere le modifiche apportate durante la migrazione, è necessario salvare il pacchetto.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Ricezione del file "%1" in corso.|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Invio del file "%1" in corso.|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|Il file "%1" esiste già.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Impossibile ottenere informazioni aggiuntive sull'errore a causa di un errore interno.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|Tentativo di eliminazione del file "%1" non riuscito. È possibile che il file non esista, che il nome del file sia stato digitato in modo non corretto o che non siano disponibili le autorizzazioni necessarie per eliminare il file.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|È in corso un tentativo di configurazione del pacchetto da una voce del Registro di sistema tramite la chiave del Registro di sistema "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|È in corso un tentativo di configurazione del pacchetto dalla variabile di ambiente "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|È in corso un tentativo di configurazione del pacchetto dal file INI "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|È in corso un tentativo di configurazione del pacchetto da SQL Server tramite la stringa di configurazione "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|È in corso un tentativo di configurazione del pacchetto dal file XML "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|È in corso un tentativo di configurazione del pacchetto dalla variabile padre "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|È in corso un tentativo di aggiornamento di SSIS dalla versione "%1" alla versione"%2". Il pacchetto sta tentando l'aggiornamento del runtime.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|È in corso un tentativo di aggiornamento di "%1". Il pacchetto sta tentando l'aggiornamento di un oggetto estensibile.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|Il pacchetto salverà i checkpoint nel file "%1" durante l'esecuzione. Il pacchetto è configurato per il salvataggio dei checkpoint.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|Il pacchetto è stato riavviato dal file del checkpoint "%1". Il pacchetto è stato configurato per il riavvio dal checkpoint.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|Il file del checkpoint "%1" è stato aggiornato per registrare il completamento del contenitore.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|Il file del checkpoint "%1" è stato eliminato dopo il completamento del pacchetto.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Avvio dell'aggiornamento del file del checkpoint "%1" in corso.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|In base alla configurazione del sistema, il numero massimo di file eseguibili simultanei è impostato su %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|Il numero massimo di file eseguibili simultanei è impostato su %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Avvio dell'esecuzione del pacchetto in corso.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|Fine dell'esecuzione del pacchetto.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|La directory "%1" è stata eliminata.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|Il file o la directory "%1" è stato eliminato.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|È in corso la sovrascrittura del database "%1" nel server di destinazione "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Il messaggio di errore "%1" verrà ignorato perché esiste già nel server di destinazione.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|Sono stati trasferiti "%1" messaggi di errore.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|L'attività ha trasferito "%1" stored procedure.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|Sono stati trasferiti "%1" oggetti.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|Nessuna stored procedure da trasferire.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|Nessuna regola da trasferire.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|Nessuna tabella da trasferire.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|Nessuna vista da trasferire.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|Nessuna funzione definita dall'utente da trasferire.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|Nessun valore predefinito da trasferire.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|Nessun tipo di dati definito dall'utente da trasferire.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|Nessuna funzione di partizione da trasferire.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|Nessuno schema di partizione da trasferire.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|Nessuno schema da trasferire.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|Nessun assembly SQL da trasferire.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|Nessuna funzione di aggregazione definita dall'utente da trasferire.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|Nessun tipo definito dall'utente (UDT) da trasferire.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|Nessuna raccolta di schemi XML da trasferire.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|Nessun account di accesso da trasferire.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|Nessun utente da trasferire.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Troncamento della tabella "%1" in corso.|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Inizio della fase Preparazione per l'esecuzione.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Inizio della fase Pre-esecuzione.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Inizio della fase Post-esecuzione.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Inizio della fase Pulizia.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Inizio della fase Convalida.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" ha scritto %2!ld! righe.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Inizio della fase Esecuzione.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|Gestione buffer ha rilevato una condizione di memoria virtuale insufficiente nel sistema, ma non ha potuto eseguire lo swapping su nessun buffer. Sono stati presi in considerazione %1!d! buffer e %2!d! erano bloccati. La memoria disponibile per la pipeline non è sufficiente, perché la memoria installata non è sufficiente o è utilizzata da altri processi oppure troppi buffer sono bloccati.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|Gestione buffer non è riuscito a eseguire una chiamata di allocazione di memoria per %3!d! byte, ma non ha potuto eseguire lo swapping su nessun buffer per alleggerire le richieste di memoria. Sono stati presi in considerazione %1!d! buffer e %2!d! erano bloccati. La memoria disponibile per la pipeline non è sufficiente, perché la memoria installata non è sufficiente o è utilizzata da altri processi oppure troppi buffer sono bloccati.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|Gestione buffer ha allocato %1!d! byte anche se è stato rilevato un numero eccessivo di richieste di memoria e i tentativi ripetuti di swapping dei buffer non sono riusciti.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 ha memorizzato nella cache %2!d! righe.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 ha memorizzato nella cache un totale di %2!d! righe.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|L'adattatore di origine file non elaborato ha aperto un file, ma il file non contiene colonne. L'adattatore non produrrà dati. L'errore potrebbe essere causato da un file danneggiato oppure indicare che ci sono zero colonne e quindi non ci sono dati.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|È disponibile un messaggio informativo OLE DB.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Le prestazioni di individuazione delle corrispondenze fuzzy possono essere migliorate se i flag FuzzyComparisonFlags di join esatto nella colonna di input "%1" vengono impostati in modo che corrispondano alle regole di confronto SQL predefinite per la colonna della tabella di riferimento "%2".  È inoltre necessario che non vengano impostati flag per la resa di tag in maiuscolo in FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Le prestazioni di individuazione delle corrispondenze fuzzy possono essere migliorate creando un indice sulla tabella di riferimento per tutte le colonne di corrispondenze esatte specificate.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|Le disposizioni per gli errori e i troncamenti non sono state controllate. Verificare che il componente sia configurato per il reindirizzamento delle righe agli output degli errori, se si desidera applicare ulteriori trasformazioni alle righe.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|La trasformazione Aggregazione ha rilevato %1!d! combinazioni di chiavi. È necessario rieseguire l'hashing dei dati perché il numero di combinazioni di chiavi è superiore al previsto. È possibile configurare il componente per evitare la ripetizione dell'hashing dei dati modificando le proprietà Keys, KeyScale e AutoExtendFactor.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|La trasformazione Aggregazione ha rilevato %1!d! valori distinct durante l'esecuzione di un'aggregazione Count Distinct su "%2". È necessario rieseguire l'hashing dei dati perché il numero di valori distinct è superiore al previsto. È possibile configurare il componente per evitare la ripetizione dell'hashing dei dati modificando le proprietà CountDistinctKeys, CountDistinctKeyScale e AutoExtendFactor.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|Elaborazione del file "%1" iniziata.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|Elaborazione del file "%1" terminata.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|Il numero totale delle righe di dati elaborate per il file "%1" è %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|Commit finale dell'operazione di inserimento dei dati in "%1" iniziato.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|Commit finale dell'operazione di inserimento dei dati in "%1" completato.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! righe aggiunte alla cache. Elaborazione delle righe in corso.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1 ha elaborato %2!u! righe nella cache. Tempo di elaborazione: %3 secondi. La cache ha utilizzato %4!I64u! byte di memoria.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1 non è riuscito a elaborare le righe della cache.  Tempo di elaborazione: %2 secondi.|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1 ha completato la preparazione della cache. Tempo di preparazione: %2 secondi.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 ha effettuato le operazioni seguenti: ha elaborato %2!I64u! righe, ha emesso %3!I64u! comandi di database nel database di riferimento e ha eseguito %4!I64u! ricerche utilizzando la cache parziale.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 ha effettuato le operazioni seguenti: ha elaborato %2!I64u! righe, ha emesso %3!I64u! comandi di database nel database di riferimento, ha eseguito %4!I64u! ricerche utilizzando la cache parziale e %5!I64u! ricerche utilizzando la cache per righe senza voci corrispondenti nella ricerca iniziale.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 sta scrivendo la cache nel file "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 ha scritto la cache nel file "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|La proprietà Dimensioni massime commit inserimento della destinazione OLE DB "%1" è impostata su 0. Questa configurazione potrebbe causare l'arresto del pacchetto di esecuzione. Per ulteriori informazioni, vedere l'argomento della Guida sensibile al contesto Editor destinazione OLE DB (pagina Gestione connessione).|  
  
##  <a name="msgGeneral"></a> Messaggi generali e messaggi di evento  
 I nomi simbolici dei messaggi di errore di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] iniziano con **DTS_MSG_** .  
  
|Codice esadecimale|Codice decimale|Nome simbolico|Descrizione|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Funzione non corretta.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|Non è possibile trovare il file specificato.|  
|0x100|256|DTS_MSG_SERVER_STARTING|È in corso l'avvio del servizio Microsoft SSIS.<br /><br /> Versione server %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Servizio Microsoft SSIS avviato.<br /><br /> Versione server %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|Tempo di attesa scaduto.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|Dati disponibili esauriti.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Impossibile avviare il servizio Microsoft SSIS.<br /><br /> Errore: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Errore durante l'arresto del servizio Microsoft SSIS.<br /><br /> Errore: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Il file di configurazione del servizio Microsoft SSIS non esiste.<br /><br /> Il servizio verrà caricato con le impostazioni predefinite.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Il file di configurazione del servizio Microsoft SSIS non è corretto.<br /><br /> Errore durante la lettura del file config: %1<br /><br /> Il servizio verrà caricato con le impostazioni predefinite.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Servizio Microsoft SSIS:<br /><br /> L'impostazione del Registro di sistema che specifica il file di configurazione non esiste.<br /><br /> Verrà eseguito un tentativo di caricamento del file config predefinito.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Servizio Microsoft SSIS: è in corso l'arresto del pacchetto in esecuzione.<br /><br /> ID istanza pacchetto: %1<br /><br /> ID pacchetto: %2<br /><br /> Nome pacchetto: %3<br /><br /> Descrizione pacchetto: %4<br /><br /> Pacchetto avviato da: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Esecuzione del pacchetto "%1" avviata.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Esecuzione del pacchetto "%1" completata.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Esecuzione del pacchetto "%1" annullata.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Esecuzione del pacchetto "%1" non riuscita.|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|Il modulo %1 non è in grado di caricare la DLL %2 per chiamare il punto di ingresso %3 a causa dell'errore %4. Il prodotto richiede l'esecuzione di tale DLL, ma non è possibile trovarla nel percorso.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|Il modulo %1 ha caricato la DLL %2, ma non è in grado di trovare il punto di ingresso %3 a causa dell'errore %4. Impossibile trovare la DLL specificata nel percorso, ma il prodotto richiede l'esecuzione di tale DLL.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Nome evento: %1<br /><br /> Messaggio: %9<br /><br /> Operatore: %2<br /><br /> Nome origine: %3<br /><br /> ID origine: %4<br /><br /> ID esecuzione: %5<br /><br /> Ora inizio: %6<br /><br /> Ora fine: %7<br /><br /> Codice dati: %8|  
  
##  <a name="msgSuccess"></a> Messaggi di operazione riuscita  
 I nomi simbolici dei messaggi di operazione riuscita di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] iniziano con **DTS_S_** .  
  
|Codice esadecimale|Codice decimale|Nome simbolico|Descrizione|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|Il valore è NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|Il valore stringa è stato troncato. Il buffer ha ricevuto una stringa troppo lunga per la colonna e la stringa è stata troncata dal buffer.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|Troncamento durante la valutazione dell'espressione. Il troncamento ha avuto luogo durante la valutazione e ciò potrebbe significare in qualsiasi punto in un passaggio intermedio.|  
  
##  <a name="msgPipeline"></a> Messaggi di errore relativi al componente flusso di dati  
 I nomi simbolici dei messaggi di errore di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] iniziano con **DTSBC_E_** , dove "BC" si riferisce alla classe di base nativa da cui quale deriva la maggior parte dei componenti flusso di dati Microsoft.  
  
|Codice esadecimale|Codice decimale|Nome simbolico|Descrizione|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|Il numero totale di output e output degli errori, %1!lu!, non è corretto. Devono essere esattamente %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Impossibile recuperare l'output con indice %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|Il numero di output degli errori, %1!lu!, non è corretto. Devono essere esattamente %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Il valore dello stato di convalida "%1!lu!" non è corretto ".  Deve essere uno dei valori disponibili nell'enumerazione DTSValidationStatus.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|Per l'input "%1!lu!" non ha un output sincrono.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|Per l'input "%1!lu!" non dispone di un output degli errori sincrono.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|Il valore HowToProcessInput %1!lu! non è valido. Deve essere uno dei valori disponibili nell'enumerazione HowToProcessInput.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Impossibile ottenere informazioni per la riga "%1!ld!", colonna"%2!ld!" dal buffer.  Codice di errore restituito: 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Impossibile impostare le informazioni per la riga"%1!ld!", colonna "%2!ld!" nel buffer.  Codice di errore restituito: 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|La proprietà "%1" non è valida.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|Impossibile trovare la proprietà %1".|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Errore durante l'assegnazione di un valore alla proprietà di sola lettura "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|%1 non consente l'inserimento di colonne di output.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|I metadati delle colonne di output non corrispondono ai metadati delle colonne di input associate.  I metadati delle colonne di output verranno aggiornati.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|Sono presenti colonne di input a cui non sono associate colonne di output. Le colonne di output verranno aggiunte.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|Sono presenti colonne di output a cui non sono associate colonne di input. Verrà annullato il mapping delle colonne di output.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|I metadati delle colonne di output non corrispondono ai metadati delle colonne di input associate.  Verrà annullato il mapping delle colonne di input.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|Sono presenti colonne di input a cui non sono associate colonne di output. Verrà annullato il mapping delle colonne di input.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|È presente una colonna di input associata a una colonna di output e tale colonna di output è già associata a un'altra colonna di input nello stesso input.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1 non consente l'inserimento di colonne di metadati esterne.|  
  
  
