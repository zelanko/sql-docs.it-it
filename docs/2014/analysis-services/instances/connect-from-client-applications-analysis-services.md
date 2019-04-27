---
title: Connessione dalle applicazioni client (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b1e0f1d4-0b87-4ad3-8172-f746fe2f16a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd6264834efbafe65bc323f0e7bd3f5eb7a0490e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730429"
---
# <a name="connect-from-client-applications-analysis-services"></a>Connessione dalle applicazioni client (Analysis Services)
  Se non si ha familiarità con Analysis Services, utilizzare le informazioni contenute in questo argomento per connettersi a un'istanza esistente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzando strumenti e applicazioni comuni. In questo argomento viene inoltre illustrato come connettersi con identità utente diverse a scopo di test.  
  
-   [Connettersi tramite SQL Server Management Studio (SSMS)](#bkmk_SSMS)  
  
-   [Connettersi tramite Excel](#bkmk_excel)  
  
-   [Connettersi tramite SQL Server Data Tools](#bkmk_SSDT)  
  
-   [Test delle connessioni](#bkmk_tshoot)  
  
 La documentazione di riferimento della stringa di connessione viene fornita separatamente. Per altre informazioni, vedere [Proprietà delle stringhe di connessione &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md).  
  
 La riuscita delle connessioni dipende da una configurazione valida della porta e dalle autorizzazioni utente appropriate. Per ulteriori informazioni su ciascun requisito, fare clic sui collegamenti riportati di seguito.  
  
-   [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> Connettersi tramite SQL Server Management Studio (SSMS)  
 Connettersi ad Analysis Services in SSMS per gestire le istanze del server e i database in modo interattivo. È inoltre possibile eseguire query MDX e XMLA per eseguire attività amministrative o recuperare dati. Diversamente da altri strumenti e applicazioni che caricano i database solo quando viene inviata una query, SSMS carica tutti i database quando ci si connette al server, presupponendo che si dispone dell'autorizzazione per visualizzare il database. Ciò significa che se nel server sono presenti numerosi database tabulari, tutti vengono caricati nella memoria di sistema quando ci si connette tramite SSMS.  
  
 È possibile testare le autorizzazioni eseguendo SSMS con un'identità utente specifica e connettersi ad Analysis Services come tale utente.  
  
 Tenere premuto il tasto MAIUSC e fare clic con il pulsante destro del mouse sul collegamento **SQL Server Management Studio** per accedere all'opzione **Esegui come altro utente** .  
  
1.  Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Nella finestra di dialogo **Connetti al server** selezionare il tipo di server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  Nella scheda Account di accesso, immettere il nome del server digitando il nome del computer in cui è in esecuzione il server. È possibile specificare il server utilizzando il nome di rete o un nome di dominio completo.  
  
     Per un'istanza denominata è necessario specificare il nome del server nel formato: nomeserver\nomeistanza. Un esempio di questa convenzione di denominazione potrebbe essere ADV-SRV062\Finanze per un server con nome di rete ADV-SRV062, in cui Analysis Services è installato come istanza denominata Finanze.  
  
     Per i server distribuiti in un cluster di failover, connettersi utilizzando il nome di rete del cluster SSAS. Questo nome viene specificato durante l'installazione di SQL Server, come **Nome rete SQL Server**. Se SSAS è stato installato come istanza denominata in un cluster di failover di Windows Server (WSFC), non si aggiunge mai il nome dell'istanza nella connessione. Questa procedura è univoca per SSAS. Diversamente, un'istanza denominata del motore del database relazionale cluster include il nome dell'istanza. Ad esempio, se SSAS e il motore di database sono stati entrambi installati come istanza denominata (Contoso-Accounting) con il nome rete SQL Server di SQL-CLU, ci si connetterebbe a SSAS utilizzando "SQL-CLU" e al motore di database come "SQL-CLU\Contoso-Accounting". Per ulteriori informazioni ed esempi, vedere [Come eseguire il clustering di SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548) .  
  
     Per i server distribuiti in un cluster con bilanciamento del carico di rete, connettersi utilizzando il nome del server virtuale di NLB.  
  
3.  Viene sempre utilizzata l'autenticazione di Windows e l'identità utente è sempre l'utente di Windows che effettua la connessione tramite Management Studio.  
  
     Affinché la connessione abbia esito positivo, è necessario disporre delle autorizzazioni per accedere al server o a un database nel server. Per la maggior parte delle attività da eseguire in Management Studio sono necessarie le autorizzazioni amministrative. Assicurarsi che l'account utilizzato per la connessione sia membro del ruolo di amministratore del server. Per altre informazioni, vedere [Concedi autorizzazioni di amministratore del Server &#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
4.  Fare clic su **Proprietà connessione** per specificare un determinato database, impostare i valori di timeout o le opzioni di crittografia. Tra le informazioni di connessione facoltative sono incluse le proprietà di connessione utilizzate solo per la connessione corrente.  
  
5.  Fare clic sulla scheda **Parametri aggiuntivi per la connessione** per impostare le proprietà di connessione non disponibili nella finestra di dialogo Connetti al server. Ad esempio, è possibile digitare `Roles=Reader` nella casella di testo.  
  
     La connessione tramite un ruolo con minori autorizzazioni consente di testare il comportamento del database quando il ruolo è attivo.  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> Connettersi tramite Excel  
 Microsoft Excel viene spesso utilizzato per analizzare i dati aziendali. Come parte di un'installazione di Excel, in Office vengono installati il provider OLE DB per Analysis Services (MSOLAP DLL), ADOMD.NET e altri provider di dati che consentono di utilizzare i dati in modo più immediato nei server di rete. Se si utilizza una versione più recente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con una versione meno recente di Excel, probabilmente sarà necessario installare provider di dati più recenti in ciascuna workstation che si connette a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [Provider di dati utilizzati per le connessioni ad Analysis Services](data-providers-used-for-analysis-services-connections.md) .  
  
 Quando si imposta una connessione su un cubo di Analysis Services o su un database modello tabulare, in Excel le informazioni di connessione vengono salvate in un file con estensione odc per l'utilizzo futuro. La connessione viene stabilita nel contesto di sicurezza dell'utente di Windows corrente. Per l'esito positivo della connessione è necessario che l'account utente disponga di autorizzazioni di lettura per il database.  
  
 Quando si utilizzano i dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in una cartella di lavoro di Excel, le connessioni vengono mantenute per la durata della richiesta di una query. Pertanto probabilmente verranno visualizzate numerose connessioni per ciascuna sessione, tenute per un periodo di tempo molto breve, durante il monitoraggio del carico di lavoro di una query da Excel.  
  
 È possibile testare le autorizzazioni avviando Excel con un'identità utente specifica.  
  
 Tenere premuto il tasto MAIUSC e fare clic con il pulsante destro del mouse sul collegamento **Excel** per accedere all'opzione **Esegui come altro utente** .  
  
1.  Nella scheda Dati di Excel, fare clic su **Da altre origini**, quindi scegliere **Da Analysis Services**. Immettere il nome del server e quindi selezionare un cubo o una prospettiva per la query.  
  
     Per i server distribuiti in un cluster con bilanciamento del carico, utilizzare il nome del server virtuale assegnato al cluster.  
  
2.  Quando si imposta una connessione in Excel, nell'ultima pagina della Connessione guidata dati è possibile specificare le impostazioni di autenticazione per Excel Services. Queste impostazioni sono utilizzate per impostare le proprietà nella cartella di lavoro se è necessario caricarla in un server SharePoint che dispone di Excel Services. Le impostazioni vengono utilizzate nelle operazioni di aggiornamento dati. Tra le opzioni sono incluse **Autenticazione di Windows**, **Servizio di archiviazione sicura** (SSS) e **Nessuna**.  
  
     È consigliabile non utilizzare **Nessuna**. Analysis Services non consente di specificare un nome utente e una password sulla stringa di connessione a meno che non si effettui la connessione a un server configurato per l'accesso HTTP. Allo stesso modo, non utilizzare SSS a meno che non si sappia che per l'ID applicazione di destinazione SSS è stato eseguito il mapping a un set di credenziali utente di Windows con accesso utente ai database di Analysis Services. Per la maggior parte degli scenari, l'utilizzo dell'opzione predefinita dell'autenticazione di Windows è la scelta ottimale per una connessione Analysis Services da Excel.  
  
 Per ulteriori informazioni, vedere [Creare una connessione o importare dati da SQL Server Analysis Services](https://go.microsoft.com/fwlink/?linkID=215150).  
  
##  <a name="bkmk_SSDT"></a> Connettersi tramite SQL Server Data Tools  
 SQL Server Data Tools si utilizzata per la compilazione di soluzioni di Business Intelligence, inclusi i modelli di Analysis Services, i report di Reporting Services e i pacchetti SSIS. Quando si compilano report o pacchetti, potrebbe essere necessario specificare una connessione ad Analysis Services.  
  
 Nei collegamenti seguenti viene illustrato come connettersi a un'istanza di Analysis Services da un progetto Server report o da un progetto di Integration Services:  
  
-   [Tipo di connessione Analysis Services per MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  Quando si utilizza SQL Server Data Tools per lavorare con un progetto esistente di Analysis Services, è possibile connettersi offline utilizzando un progetto locale o un progetto con controllo della versione o connettersi in modalità online per aggiornare gli oggetti di Analysis Services mentre il database è in esecuzione. Per ulteriori informazioni, vedere [Connect in Online Mode to an Analysis Services Database](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md). Più comunemente, le connessioni da [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sono in modalità progetto, dove le modifiche vengono distribuite al database solo quando si distribuisce in modo esplicito il progetto.  
  
##  <a name="bkmk_tshoot"></a> Test delle connessioni  
 È possibile utilizzare SQL Server Profiler per il monitoraggio delle connessioni ad Analysis Services. Gli eventi Audit Login e Audit Logout forniscono l'evidenza di una connessione. La colonna Identity indica il contesto di sicurezza in cui la connessione viene eseguita.  
  
1.  Avviare **SQL Server Profiler** nell'istanza di Analysis Services e quindi avviare una nuova traccia.  
  
2.  In Selezione eventi, verificare che `Audit Login` e `Audit Logout` siano selezionati nella sezione Controllo di sicurezza.  
  
3.  Connettersi ad Analysis Services tramite un servizio di applicazione (ad esempio SharePoint o Reporting Services) da un computer client remoto. L'evento Audit Login visualizzerà l'identità dell'utente che si connette ad Analysis Services.  
  
 Gli errori di connessione vengono spesso tracciati per una configurazione del server incompleta o non valida. Controllare per prima cosa sempre la configurazione del server:  
  
-   Eseguire il ping del server da un computer remoto per assicurarsi che autorizzi le connessioni remote.  
  
-   **Le regole del firewall del server consentono le connessioni in ingresso dai client nello stesso dominio**  
  
     Fatta eccezione per PowerPivot per SharePoint, tutte le connessioni a un server remoto richiedono la configurazione del firewall per consentire l'accesso alla porta su cui è in ascolto Analysis Services. Se vengono restituiti errori di connessione, verificare che la porta sia accessibile e che siano state concesse autorizzazioni utente per i database appropriati.  
  
     Per testare, utilizzare Excel o SSMS in un computer remoto, specificando l'indirizzo IP e la porta utilizzati dall'istanza di Analysis Services. Se è possibile connettersi, le regole del firewall sono valide per l'istanza e l'istanza consente le connessioni remote.  
  
     Inoltre, quando si utilizza TCP/IP per il protocollo di connessione, Analysis Services richiede connessioni client che provengono dallo stesso dominio o da un dominio trusted. Se le connessioni vengono propagate attraverso i limiti di sicurezza, è necessario configurare l'accesso HTTP. Per altre informazioni, vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
-   È possibile connettersi utilizzando solo alcuni strumenti ma non altri? Il problema potrebbe essere costituito dall'errata versione di una libreria client. È possibile recuperare le librerie client dalla pagina di download di SQL Server Feature Pack.  
  
 Le risorse che consentono di risolvere gli errori di connessione includono:  
  
 [Risoluzione di problemi di connettività comuni negli scenari di connettività di SQL Server 2005 Analysis Services](https://technet.microsoft.com/library/cc917670.aspx). Il documento è stato scritto da alcuni anni, ma le informazioni e le metodologie sono comunque valide.  
  
## <a name="see-also"></a>Vedere anche  
 [Connetti ad Analysis Services](connect-to-analysis-services.md)   
 [Metodologie di autenticazione supportate da Analysis Services](authentication-methodologies-supported-by-analysis-services.md)   
 [Rappresentazione &#40;SSAS tabulare&#41;](../tabular-models/impersonation-ssas-tabular.md)   
 [Creare un'origine dati &#40;SSAS multidimensionale&#41;](../multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
