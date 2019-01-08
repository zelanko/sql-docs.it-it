---
title: PowerShell di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cec716534e6cffa7cc44aafb96ec0541e49d6e48
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355911"
---
# <a name="analysis-services-powershell"></a>PowerShell per Analysis Services
  In [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] sono inclusi cmdlet e un provider PowerShell per Analysis Services (SQLAS) in modo che sia possibile utilizzare Windows PowerShell per la navigazione, l'amministrazione e l'esecuzione di query sugli oggetti di Analysis Services.  
  
 PowerShell per Analysis Services è costituito dagli elementi seguenti:  
  
-   Provider per `SQLAS` utilizzato per la navigazione all'interno della gerarchia AMO (Analysis Management Object).  
  
-   Cmdlet `Invoke-ASCmd` utilizzato per l'esecuzione di script MDX, DMX o XMLA.  
  
-   Cmdlet specifici dell'attività per operazioni di routine, quali elaborazione, gestione dei ruoli, gestione delle partizioni, nonché per backup e ripristino.  
  
## <a name="in-this-article"></a>Contenuto dell'articolo  
 [Prerequisiti](#bkmk_prereq)  
  
 [Versioni supportate e le modalità di Analysis Services](#bkmk_vers)  
  
 [Requisiti di autenticazione e considerazioni sulla sicurezza](#bkmk_auth)  
  
 [Attività di PowerShell di Analysis Services](#bkmk_tasks)  

Per altre informazioni sulla sintassi ed esempi, vedere [Analysis Services PowerShell Reference](/sql/analysis-services/powershell/analysis-services-powershell-reference).

##  <a name="bkmk_prereq"></a> Prerequisiti  
 È necessario installare Windows PowerShell 2.0. Questa applicazione è installata per impostazione predefinita nelle versioni più recenti dei sistemi operativi Windows. Per altre informazioni, vedere [installare Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (https://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 È necessario installare una funzionalità di SQL Server che include il modulo SQL Server PowerShell (SQLPS) e librerie client. Il modo più semplice per effettuare questa operazione consiste nell'installare SQL Server Management Studio che include automaticamente la funzionalità PowerShell e librerie client. Nel modulo SQL Server PowerShell (SQLPS) sono inclusi tutti i cmdlet e i provider PowerShell per tutte le funzionalità di SQL Server, tra cui il modulo SQLASCmdlets e il provider SQLAS utilizzati per la navigazione nella gerarchia di oggetti di Analysis Services.  
  
 È necessario importare il **SQLPS** modulo prima di poter usare il `SQLAS` provider e dai cmdlets. Il provider per SQLAS è un'estensione del `SQLServer` provider. Sono disponibili diversi modi per importare il modulo SQLPS. Per altre informazioni, vedere [Importare il modulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
 Per l'accesso remoto a un'istanza di Analysis Services è necessaria l'abilitazione dell'amministrazione remota e la condivisione di file. Per altre informazioni, vedere [abilitare l'amministrazione remota](#bkmk_remote) in questo argomento.  
  
##  <a name="bkmk_vers"></a> Versioni e modalità supportate di Analysis Services  
 Attualmente, PowerShell per Analysis Services è supportato in qualsiasi edizione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services in esecuzione in Windows Server 2008 R2, Windows Server 2008 SP1 o Windows 7.  
  
 Nella tabella seguente viene mostrata la disponibilità di PowerShell per Analysis Services in contesti diversi.  
  
|Contesto|Disponibilità della funzionalità PowerShell|  
|-------------|-------------------------------------|  
|Istanze e database multidimensionali|Supportata per l'amministrazione locale e remota.<br /><br /> La partizione di tipo merge richiede una connessione locale.|  
|Istanze e database tabulari|Supportata per l'amministrazione locale e remota.<br /><br /> Per altre informazioni, vedere un blog di agosto 2011 [gestione di modelli tabulari tramite PowerShell](https://go.microsoft.com/fwlink/?linkID=227685).|  
|Database e istanze di PowerPivot per SharePoint|Supporto limitato. È possibile utilizzare connessioni HTTP e il provider per SQLAS per visualizzare informazioni sulle istanze e sui database.<br /><br /> Tuttavia, l'utilizzo che i cmdlet non è supportato. Non utilizzare PowerShell per Analysis Services per eseguire il backup e ripristino in memoria del database PowerPivot, né aggiungere o rimuovere ruoli, elaborare dati o eseguire script XMLA arbitrario.<br /><br /> Per scopi di configurazione, in PowerPivot per SharePoint è disponibile il supporto PowerShell predefinito che viene fornito separatamente. Per altre informazioni, vedere [informazioni di riferimento di PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).|  
|Connessioni native a cubi locali<br /><br /> "Dati Source=c:\backup\test.cub"|Non supportato.|  
|Connessioni HTTP a file di connessione (con estensione bism) di Business Intelligence Semantic Model in SharePoint<br /><br /> "Data Source =http://server/shared_docs/name.bism"|Non supportato.|  
|Connessioni incorporate ai database PowerPivot<br /><br /> "Data Source = $Embedded$"|Non supportato.|  
|Contesto del server locale nelle stored procedure di Analysis Services<br /><br /> "Data Source = *"|Non supportato.|  
  
##  <a name="bkmk_auth"></a> Requisiti di autenticazione e considerazioni sulla sicurezza  
 Quando si stabilisce la connessione ad Analysis Services, è necessario creare tale connessione utilizzando un'identità utente di Windows. Nella maggior parte dei casi, una connessione viene creata tramite la sicurezza integrata di Windows, dove l'identità dell'utente corrente imposta il contesto di sicurezza nel quale vengono eseguite le operazioni del server. Tuttavia, metodi di autenticazione aggiuntivi diventano disponibili quando si configura l'accesso HTTP ad Analysis Services. In questa sezione viene illustrato in che modo il tipo di connessione determina quali opzioni di autenticazione è possibile utilizzare.  
  
 Le connessioni ad Analysis Services sono caratterizzate come connessioni native o come connessioni HTTP. Una connessione nativa è una connessione diretta da un'applicazione client al server. In una sessione di PowerShell, il client PowerShell utilizza il provider OLE DB per Analysis Services per connettersi direttamente a un'istanza di Analysis Services. Una connessione nativa viene sempre creata tramite la sicurezza integrata di Windows, dove PowerShell per Analysis Services viene eseguito come utente corrente. In Analysis Services non è supportata la rappresentazione. Se si desidera eseguire un'operazione come utente specifico, è necessario avviare la sessione di PowerShell con il nome di tale utente.  
  
 Le connessioni HTTP vengono effettuate indirettamente tramite IIS, consentendo l'utilizzo di opzioni di autenticazione aggiuntive, ad esempio l'autenticazione di base, per connettersi a un'istanza di Analysis Services. Poiché in IIS è supportata la rappresentazione, è possibile fornire una stringa di connessione che includa le credenziali utilizzate da IIS per la rappresentazione quando viene stabilita una connessione. Per fornire le credenziali, è possibile usare il parametro - Credential.  
  
 **Usando il parametro - Credential in PowerShell**  
  
 -Credenziale parametro accetta un oggetto PSCredential che specifica un nome utente e password. In PowerShell per Analysis Services,-Credential parametro è disponibile per i cmdlet che effettuano una richiesta di connessione ad Analysis Services, a differenza dei cmdlet eseguiti nel contesto di una connessione esistente. I cmdlet che effettuano una richiesta di connessione includono Invoke-ASCmd, Backup-ASDatabase e Restore-ASDatabase. Per questi cmdlet,-Credential parametro può essere usato, presupponendo che siano soddisfatti i criteri seguenti:  
  
1.  Il server viene configurato per l'accesso HTTP, ovvero in IIS viene gestita la connessione, vengono letti il nome utente e la password e viene rappresentata l'identità di tale utente durante la connessione ad Analysis Services. Per altre informazioni, vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)(Autenticazione di Microsoft Business Intelligence e la delega dell'identità).  
  
2.  La directory virtuale IIS creata per accesso HTTP ad Analysis Services viene configurata per l'autenticazione di base.  
  
3.  Il nome utente e la password forniti dall'oggetto Credential vengono risolti nell'identità di un utente di Windows. Questa identità viene utilizzata in Analysis Services come utente corrente. Se l'utente non è un utente di Windows, o non dispone di autorizzazioni sufficienti per eseguire l'operazione richiesta, la richiesta non verrà completata.  
  
 Per creare un oggetto Credential, è possibile utilizzare il cmdlet Get-Credential per raccogliere le credenziali dall'operatore. È quindi possibile utilizzare l'oggetto Credential in un comando che stabilisce la connessione ad Analysis Services. Nell'esempio seguente vien illustrato un approccio. In questo esempio la connessione viene stabilita a un'istanza locale configurata per l'accesso HTTP.  
  
```  
PS SQLSERVER:\SQLAS\HTTP_DS> $cred = Get-credential adventureworks\dbadmin  
PS SQLSERVER:\SQLAS\HTTP_DS> Invoke-ASCmd -Inputfile:"c:\discoverconnections.xmla" -Credential:$cred  
```  
  
 Quando si utilizza l'autenticazione di base, è necessario utilizzare sempre HTTPS con SSL in modo che nome utente e password vengano inviati su una connessione crittografata. Per altre informazioni, vedere [configurare Secure Sockets Layer in IIS 7.0](https://go.microsoft.com/fwlink/?linkID=184299) e [configurare l'autenticazione di base (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=230776).  
  
 Ricordare che credenziali, query e comandi forniti in PowerShell vengono passati invariati al livello di trasporto. L'inclusione di contenuto riservato negli script aumenta il rischio di un attacco di tipo injection dannoso.  
  
 **Fornire una password come oggetto Microsoft.Secure.String**  
  
 Alcune operazioni, ad esempio backup e ripristino, supportano opzioni di crittografia che vengono attivate quando si specifica una password nel comando. La password indica ad Analysis Services di crittografare o decrittografare il file di backup. In Analysis Services viene creata un'istanza di questa password come oggetto stringa sicura. Nell'esempio seguente viene illustrato come raccogliere una password dall'operatore in fase di esecuzione.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd = read-host -AsSecureString -Prompt "Password"  
Password: ****  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd -is [System.IDisposable]   
True  
```  
  
 È possibile a questo punto eseguire il backup o ripristinare un file di database crittografato, passando la variabile $pwd al parametro password. Per visualizzare un esempio completo che combina quanto illustrato con altri cmdlet, vedere [cmdlet Backup-ASDatabase](/sql/analysis-services/powershell/backup-asdatabase-cmdlet) e [cmdlet Restore-ASDatabase](/sql/analysis-services/powershell/restore-asdatabase-cmdlet).
  
 Come passaggio di completamento, rimuovere sia la password che la variabile dalla sessione.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default> Remove-Variable -Name pwd  
```  
  
##  <a name="bkmk_tasks"></a> Attività di PowerShell di Analysis Services  
 È possibile eseguire PowerShell per Analysis Services dalla shell di gestione di Windows PowerShell o da un prompt dei comandi di Windows. L'esecuzione di PowerShell per Analysis Services da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] non è supportata.  
  
 In questa sezione vengono descritte le attività comuni per l'utilizzo di PowerShell per Analysis Services.  
  
-   [L'analisi del carico cmdlet e Provider di servizi](#bkmk_load)  
  
-   [Abilitare l'amministrazione remota](#bkmk_remote)  
  
-   [Connettersi a una di Analysis Services oggetto](#bkmk_connect)  
  
-   [Amministrare il servizio](#bkmk_admin)  
  
-   [Visualizzare la Guida di PowerShell per Analysis Services](#bkmk_help)  
  
###  <a name="bkmk_load"></a> L'analisi del carico cmdlet e Provider di servizi  
 Il provider per Analysis Services è un'estensione del provider radice per SQL Server disponibile quando si importa il modulo SQLPS. I cmdlet di Analysis Services vengono caricati contemporaneamente. È possibile caricarli anche in modo indipendente se si desidera utilizzarli senza il provider.  
  
-   Eseguire il cmdlet Import-module per caricare SQLPS in cui sono incluse tutte le funzionalità di PowerShell per Analysis Services. Se non è possibile importare il modulo, è possibile impostare temporaneamente i criteri di esecuzione su senza limitazioni relativamente al caricamento del modulo. Per altre informazioni, vedere [Importare il modulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
    ```  
    Import-module "sqlps"  
    ```  
  
     In alternativa, utilizzare `import-module "sqlps" -disablenamechecking` per eliminare l'avviso sui nomi di verbi non approvati.  
  
-   Per caricare solo i cmdlet di Analysis Services per attività specifiche, senza il provider Analysis Services o il cmdlet Invoke-ASCmd, è possibile caricare il modulo SQLASCmdlets come operazione indipendente.  
  
    ```  
    Import-module "sqlascmdlets"  
    ```  
  
###  <a name="bkmk_remote"></a> Abilitare l'amministrazione remota  
 Prima che sia possibile utilizzare PowerShell per Analysis Services con un'istanza di Analysis Services remota, è necessario abilitare innanzitutto l'amministrazione remota e la condivisione di file. L'errore seguente indica un problema di configurazione del firewall: "Il server RPC non è disponibile. (Eccezione da HRESULT: 0x800706ba) ".  
  
1.  Verificare che sia il computer locale sia quello remoto dispongano delle versioni di [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] degli strumenti client e server.  
  
2.  Nel server remoto in cui viene ospitata un'istanza di Analysis Services, aprire la porta TCP 2383 in Windows Firewall. Se Analysis Services è installato come istanza denominata o si utilizza una porta personalizzata, il numero di porta sarà diverso. Per altre informazioni, vedere [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
3.  Nel server remoto, verificare che siano avviati i servizi seguenti:  Servizio di Remote Procedure Call (RPC), servizio NetBIOS Helper di TCP/IP, il servizio Strumentazione gestione Windows (WMI), servizio Gestione remota Windows (WS-Management).  
  
4.  Nel server remoto avviare lo snap-in Editor oggetti Criteri di gruppo (gpedit.msc).  
  
5.  Aprire Configurazione computer, Modelli amministrativi, Rete, Connessioni di rete, Windows Firewall e Profilo di dominio.  
  
6.  Fare doppio clic su **Windows Firewall: Consenti eccezione amministrazione remota in ingresso**, selezionare **Enabled**, quindi fare clic su **OK**.  
  
7.  Fare doppio clic su **Windows Firewall: Consenti eccezione di condivisione stampanti e file in ingresso**, selezionare **Enabled**, quindi fare clic su **OK**.  
  
8.  Nel computer locale con gli strumenti client, usare i cmdlet seguenti per verificare l'amministrazione remota, sostituendo il nome effettivo del server per il *nome-server-remoto* segnaposto. Omettere il nome dell'istanza se Analysis Services è installato come istanza predefinita. È necessario aver importato precedentemente il modulo SQLPS affinché il comando venga eseguito correttamente.  
  
    ```  
    PS SQLSERVER:\> cd sqlas  
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 In alcuni casi potrebbe essere necessaria una configurazione aggiuntiva. Potrebbe essere necessario digitare quanto riportato di seguito nel server remoto prima che sia possibile eseguire comandi per questo server da un altro computer:  
  
```  
Enable-psremoting  
```  
  
  
###  <a name="bkmk_connect"></a> Connettersi a una di Analysis Services oggetto  
 Il provider PowerShell per Analysis Services supporta la navigazione all'interno della gerarchia di oggetti di Analysis Services e consente di impostare il contesto per l'esecuzione dei comandi. Il provider è un'estensione del provider radice per SQLSERVER disponibile tramite il modulo SQLPS. Dopo aver caricato questo modulo, è possibile passare al percorso.  
  
 È possibile connettersi a un'istanza locale o remota, ma alcuni cmdlet vengono eseguiti solo in un'istanza locale, vale a dire partizione di tipo merge. È possibile utilizzare una connessione nativa o una HTTP per i server Analysis Services configurati per l'accesso HTTP. Nelle illustrazioni seguenti viene mostrato il percorso di navigazione per le connessioni native e HTTP. Nelle illustrazioni seguenti viene mostrato il percorso di navigazione per le connessioni native e HTTP.  
  
 **Connessioni native ad Analysis Services**  
  
 ![Connessione nativa ad Analysis Services](media/ssas-powershell-nativeconnection.gif "connessione nativa ad Analysis Services")  
  
 L'esempio seguente è una dimostrazione della modalità di utilizzo di una connessione nativa per spostarsi all'interno di una gerarchia di oggetti. Dal provider è possibile eseguire un comando `dir` per visualizzare le informazioni sull'istanza. È possibile utilizzare `cd` per visualizzare gli oggetti di questa istanza.  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 Dovrebbe essere le raccolte seguenti: Gli assembly, database, ruoli e tracce. Continuando a utilizzare `cd` e `dir`, è possibile visualizzare il contenuto di ciascuna raccolta.  
  
 **Connessioni HTTP ad Analysis Services**  
  
 ![Connessione HTTP ad Analysis Services](media/ssas-powershell-httpconnection.gif "connessione HTTP ad Analysis Services")  
  
 Le connessioni HTTP sono utili se è configurato il server per l'accesso HTTP utilizzando le istruzioni riportate in questo argomento: [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 Presupponendo un URL del server di http://localhost/olap/msmdpump.dll, una connessione potrebbe essere simile al seguente:  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName "http://localhost/olap/msmdpump.dll"  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 Dovrebbe essere le raccolte seguenti: Gli assembly, database, ruoli e tracce. Se non è possibile visualizzare il contenuto di queste raccolte, controllare le impostazioni di autenticazione nella directory virtuale OLAP. Verificare che l'accesso anonimo sia disabilitato. Se si utilizza Autenticazione di Windows, assicurarsi che l'account utente di Windows disponga delle autorizzazioni amministrative per l'istanza di Analysis Services.  
  
###  <a name="bkmk_admin"></a> Amministrare il servizio  
 Verificare che il servizio sia in esecuzione. Vengono restituiti lo stato, il nome e il nome visualizzato dei servizi SQL Server, inclusi Analysis Services (MSSQLServerOLAPService) e il motore di database.  
  
```  
Get-service mssql*  
```  
  
 Vengono restituite le proprietà su un processo, inclusi ID processo, conteggio degli handle e utilizzo della memoria:  
  
```  
Get-process msmdsrv  
```  
  
 Viene riavviato il servizio quando il cmdlet riportato di seguito viene eseguito dalla shell dell'amministratore:  
  
```  
Restart-service mssqlserverolapservice  
```  
  
###  <a name="bkmk_help"></a> Visualizzare la Guida di PowerShell per Analysis Services  
 Utilizzare alcuni dei cmdlet seguenti per verificare la disponibilità del cmdlet e per ottenere ulteriori informazioni su servizi, processi e oggetti.  
  
1.  Tramite `Get-help` viene restituita la Guida incorporata per un cmdlet di Analysis Services, tra cui examples:  
  
    ```  
    Get-help invoke-ascmd -examples  
    ```  
  
2.  Tramite `Get-command` viene restituito un elenco degli undici cmdlet di PowerShell per Analysis Services:  
  
    ```  
    get-command -module SQLASCmdlets  
    ```  
  
3.  Tramite `Get-member` vengono restituiti metodi o proprietà di un servizio o processo.  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Property  
    ```  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Method  
    ```  
  
    ```  
    Get-process msmdsrv | get-member -type Property  
    ```  
  
4.  `Get-member` può essere utilizzato anche per restituire proprietà o metodi di un oggetto, ad esempio metodi AMO nell'oggetto server, utilizzando il provider per SQLAS per specificare l'istanza del server.  
  
    ```  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | get-member -type Method  
    ```  
  
5.  Tramite `Get-PSdrive` viene restituito un elenco dei provider attualmente installati. Se è stato importato il modulo SQLPS, verrà visualizzato il provider per `SQLServer` nell'elenco. SQLAS è parte del provider per SQLServer e non viene mai visualizzato separatamente nell'elenco:  
  
    ```  
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server PowerShell](../database-engine/install-windows/install-sql-server-powershell.md)   
 [Gestire i modelli tabulari tramite PowerShell (blog)](https://go.microsoft.com/fwlink/?linkID=227685)   
 [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
