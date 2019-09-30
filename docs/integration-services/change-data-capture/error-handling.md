---
title: Gestione degli errori | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a4aebf354f999b26be59efc2f3c25a205dd3d9d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298783"
---
# <a name="error-handling"></a>Gestione degli errori

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Un'istanza di Oracle CDC estrae le modifiche da un singolo database di origine Oracle (un cluster Oracle RAC è considerato un singolo database) e scrive le modifiche di cui è stato eseguito il commit per modificare le tabelle in un database CDC nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 Un'istanza di CDC mantiene il proprio stato in una tabella di sistema denominata **cdc.xdbcdc_state**. È possibile eseguire query su questa tabella ogni volta che è necessario trovare lo stato dell'istanza di CDC. Per altre informazioni sulla tabella cdc.xdbcdc_state, vedere [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state).  
  
 Nella tabella seguente vengono descritti gli stati dell'istanza di CDC nella tabella xdbcdc_state.  
  
 Per ogni stato vengono mostrate le due indicazioni seguenti per le colonne corrispondenti nella tabella cdc.xdbcdc_state:  
  
-   L'istanza non è attiva, ovvero non è attualmente gestita da alcun processo di Windows. Se il valore della colonna **active** è 1, è in esecuzione un sottoprocesso del servizio Oracle CDC che gestisce questa istanza di Oracle CDC.  
  
-   Se il valore della colonna **error** è 0, l'istanza di Oracle CDC non si trova in una condizione di errore. Se il valore della colonna **error** è 1, un errore impedisce l'elaborazione delle modifiche da parte dell'istanza di Oracle CDC.  
  
     Se la colonna **error** contiene il valore 1 e il valore della colonna **active** è anch'esso 1, si è verificato un errore reversibile per l'istanza di Oracle CDC che può essere risolto automaticamente. Se la colonna error contiene un valore 1 e la colonna active il valore 0, nella maggior parte dei casi potrebbe essere necessario ricorrere a una soluzione alternativa manuale per risolvere il problema prima di poter riprendere l'elaborazione.  
  
 Nella tabella seguente vengono descritti i vari codici di stato che è possibile ritrovare nella tabella dello stato dell'istanza di Oracle CDC.  
  
|Stato|Codice di stato attivo|Codice di stato errore|Descrizione|Stato secondario|  
|------------|------------------------|-----------------------|-----------------|---------------|  
|ABORTED|0|1|L'istanza di Oracle CDC non è in esecuzione. Lo stato secondario ABORTED indica che l'istanza di Oracle CDC era ACTIVE e che si è arrestata in modo imprevisto.|Lo stato secondario ABORTED viene stabilito dall'istanza principale del servizio Oracle CDC quando viene rilevato che l'istanza di Oracle CDC non è in esecuzione mentre il relativo stato è ACTIVE.|  
|error|0|1|L'istanza di Oracle CDC non è in esecuzione. Lo stato ERROR indica che l'istanza di CDC era ACTIVE, ma che in seguito a un errore reversibile è stata disabilitata.|MISCONFIGURED: è stato rilevato un errore di configurazione irreversibile.<br /><br /> PASSWORD-REQUIRED: non è stata impostata alcuna password per Change Data Capture Designer per Oracle di Attunity oppure la password configurata non è valida. Il problema può essere dovuto a una modifica alla password della chiave asimmetrica del servizio.|  
|RUNNING|1|0|L'istanza di CDC è in esecuzione ed è in corso l'elaborazione dei record delle modifiche.|IDLE: tutti i record delle modifiche sono stati elaborati e archiviati nelle tabelle di controllo di destinazione ( **_CT**). Non è presente alcuna transazione attiva con le tabelle di controllo.<br /><br /> PROCESSING: è in corso l'elaborazione di alcuni record delle modifiche che non sono ancora stati scritti nelle tabelle di controllo ( **_CT**).|  
|STOPPED|0|0|L'istanza di CDC non è in esecuzione.|Lo stato secondario STOP indica che l'istanza di CDC era ACTIVE e che è stata arrestata in modo corretto.|  
|SUSPENDED|1|1|L'istanza di CDC è in esecuzione ma l'elaborazione è stata sospesa in seguito a un errore reversibile.|DISCONNECTED: non è possibile stabilire la connessione con il database Oracle di origine. L'elaborazione verrà ripresa dopo il ripristino della connessione.<br /><br /> STORAGE: lo spazio di archiviazione è esaurito. L'elaborazione verrà ripresa non appena sarà nuovamente disponibile dello spazio di archiviazione. In alcuni casi è possibile che questo stato non venga visualizzato perché non è possibile aggiornare la tabella dello stato.<br /><br /> LOGGER: il logger è connesso a Oracle, ma non è in grado di leggere i log delle transazioni di Oracle a causa di un problema temporaneo.|  
|DATAERROR|x|x|Questo codice di stato viene usato unicamente per la tabella **xdbcdc_trace** . e non compare nella tabella **xdbcdc_state** . I record di traccia con questo stato indicano un problema con un record di log Oracle. Il record di log danneggiato viene archiviato nella colonna **data** come BLOB.|BADRECORD: non è possibile analizzare il record di log collegato.<br /><br /> CONVERT-ERROR: non è possibile convertire i dati di alcune colonne nelle colonne di destinazione della tabella di acquisizione. È possibile che questo stato si verifichi solo se nella configurazione è stato specificato che gli errori di conversione devono produrre record di traccia.|  
  
 Poiché lo stato del servizio Oracle CDC viene archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile che in alcuni casi il valore dello stato nel database non rifletta lo stato effettivo del servizio. Lo scenario più comune si verifica quando il servizio perde la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e per un qualche motivo non è in grado di riprenderla. In questo caso, lo stato archiviato in **cdc.xdbcdc_state** non risulta più aggiornato. Se il timestamp dell'ultimo aggiornamento (UTC) risale a più di un minuto prima, lo stato non è probabilmente aggiornato. In questo caso, utilizzare il Visualizzatore eventi di Windows per trovare informazioni aggiuntive sullo stato del servizio.  
  
## <a name="error-handling"></a>Gestione degli errori  
 In questa sezione viene illustrato come vengono gestiti gli errori dal servizio Oracle CDC.  
  
### <a name="logging"></a>Registrazione  
 Il servizio Oracle CDC crea informazioni sugli errori in una delle posizioni seguenti.  
  
-   Registro eventi di Windows, utilizzato per la registrazione degli errori e per indicare gli eventi del ciclo di vita del servizio Oracle CDC, ovvero avvio, arresto e (ri)connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
-   Tabella MSXDBCDC.dbo.xdbcdc_trace, utilizzata per le operazioni di registrazione generale e di traccia effettuate dal processo principale del servizio Oracle CDC.  
  
-   Tabella \<cdc-database>.cdc.xdbcdc_trace, usata per le operazioni di registrazione generale e di traccia effettuate dalle istanze di Oracle CDC. Ciò significa che gli errori correlati a un'istanza specifica di Oracle CDC vengono registrati nella tabella di traccia dell'istanza.  
  
 Le informazioni vengono registrate dal servizio Oracle CDC quando il servizio:  
  
-   Viene avviato o arrestato da Gestione controllo servizi.  
  
-   Non è in grado di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata e una connessione viene stabilita correttamente dopo un errore.  
  
-   Rileva un errore durante l'avvio delle istanze del servizio Oracle CDC.  
  
-   Rileva che un'istanza di Oracle CDC è stata interrotta.  
  
-   Rileva un errore imprevisto.  
  
 Le informazioni vengono registrate dall'istanza di CDC quando l'istanza:  
  
-   Viene abilitata o disabilitata.  
  
-   Rileva un errore.  
  
-   Risolve un errore reversibile.  
  
 Anche la tabella di traccia viene utilizzata per registrare informazioni di traccia dettagliate per la risoluzione dei problemi.  
  
### <a name="handling-source-oracle-connection-errors"></a>Gestione degli errori di connessione al database Oracle di origine  
 Per il servizio Oracle CDC è necessario disporre di una connessione persistente al database Oracle di origine. Molti errori di connessione non correlati alla configurazione del servizio, ad esempio gli errori di rete, sono considerati temporanei. Di conseguenza, se il servizio Oracle CDC non è in grado di stabilire la connessione al database Oracle all'avvio o in seguito a una disconnessione, lo stato del servizio diventa SUSPENDED/DISCONNECTED e ha inizio un ciclo di tentativi di riconnessione a intervalli regolari. Quando viene ristabilita la connessione, l'elaborazione può continuare.  
  
 Altri tipi di errori di connessione non sono temporanei, ad esempio credenziali non corrette, privilegi insufficienti e indirizzo del database errato. Quando si verificano questi errori, il servizio Oracle CDC viene impostato sullo stato ERROR/MISCONFIGURED o ERROR/PASSWORD-REQUIRED e il servizio viene disabilitato. Dopo che l'errore sottostante è stato risolto, è necessario abilitare manualmente l'istanza di Oracle CDC per poter riprendere l'elaborazione.  
  
 Nei casi in cui non è chiaro se l'errore è temporaneo, è preferibile presupporre che lo sia.  
  
### <a name="handling-target-sql-server-connection-errors"></a>Gestione degli errori di connessione di SQL Server di destinazione  
 Per il servizio Oracle CDC è necessario disporre di una connessione persistente all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione. Questa connessione viene utilizzata per le operazioni seguenti:  
  
-   Assicurarsi che non vi siano altri servizi con lo stesso nome che utilizzano questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Verificare quale istanza di Oracle CDC è abilitata o disabilitata e avviare (o arrestare) i relativi sottoprocessi.  
  
 Quando il servizio stabilisce una connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione e accerta che sia l'unico servizio Oracle CDC con questo nome a essere in funzione, può verificare quali istanze di Oracle CDC sono abilitate e avviare i relativi processi di gestione. In seguito questi processi verranno arrestati dopo essere stati disabilitati. Le istanze di Oracle CDC utilizzano le connessioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per utilizzare il database CDC dell'istanza di Oracle CDC.  
  
 Il fatto che gli errori siano o meno temporanei influisce sulla modalità di gestione degli stessi quando viene persa la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 Per gli errori non temporanei noti, ad esempio credenziali errate, privilegi insufficienti, informazioni di connessione non corrette, viene registrato un errore nel registro eventi di Windows e il servizio viene arrestato (non è più in grado di scrivere nella tabella di traccia perché la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è andata persa). In questo caso, l'utente deve risolvere l'errore e riavviare il servizio di Windows Oracle CDC.  
  
 Per gli errori temporanei e quelli imprevisti, vengono effettuati diversi tentativi per eseguire l'operazione e se l'errore persiste per un periodo di tempo significativo, il servizio arresta i sottoprocessi dell'istanza di CDC e torna al tentativo di connessione iniziale. Nel frattempo è possibile che un servizio Oracle CDC in un altro computer abbia assunto il controllo del servizio CDC denominato.  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>Gestione degli errori di spazio di archiviazione esaurito di SQL Server di destinazione  
 Quando il servizio Oracle CDC rileva l'impossibilità di inserire nuovi dati delle modifiche nel database CDC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione, scrive un avviso nel registro eventi e tenta di inserire un record di traccia (anche se l'operazione potrebbe non riuscire per lo stesso motivo). Verranno quindi effettuati tanti tentativi quanti saranno sufficienti per completare correttamente l'operazione.  
  
### <a name="handling-oracle-cdc-errors"></a>Gestione degli errori di Oracle CDC  
 L'istanza di Oracle CDC legge il log delle transazioni Oracle e lo elabora. Se durante l'elaborazione di CDC si verifica un errore, tale errore viene riportato nella tabella **cdc.xdbcdc_state** e l'utente deve intervenire manualmente in base a quanto riportato.  
  
 È ad esempio possibile che l'istanza di Oracle CDC rimanga inattiva per un periodo di tempo prolungato e che i file di log delle transazioni non siano più disponibili. In questo caso, Oracle DBA deve ripristinare i log necessari affinché nell'istanza di Oracle CDC venga ripresa l'elaborazione.  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>Gestione degli errori imprevisti dell'istanza di Oracle CDC  
 Il servizio Oracle CDC monitora i sottoprocessi dell'istanza di CDC. Quando un sottoprocesso dell'istanza di CDC viene interrotto, il servizio CDC lo disabilita nella tabella MSXDBCDC.dbo.xdbcdc_databases e ne aggiorna lo stato cdc.xdbcdc_state su ABORTED. In questo caso, viene utilizzata la finestra di dialogo Segnalazione errori Windows standard per segnalare questo errore a scopo di ulteriore analisi.  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione Change Data Capture per Oracle di Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Istanza di Oracle CDC](../../integration-services/change-data-capture/the-oracle-cdc-instance.md)  
  
  
