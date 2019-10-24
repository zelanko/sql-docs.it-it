---
title: PowerPivot per SharePoint di aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78112ef90eab7b6b6dd881474d04a350f6ea6ca0
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783164"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>Aggiornare PowerPivot per SharePoint
  In questo argomento vengono riepilogati i passaggi necessari per aggiornare una distribuzione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] a [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]. I passaggi specifici dipendono dalla versione di SharePoint attualmente in esecuzione nell'ambiente e includono il componente aggiuntivo PowerPivot per SharePoint (**spspPowerPivot. msi**).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 Per le note sulla versione, vedere le [Note sulla versione di SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  

  
## <a name="background"></a>Informazioni preliminari  
  
-   Se viene eseguito l'aggiornamento di una farm SharePoint 2010 multiserver in cui sono incluse due o più istanze di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , è necessario eseguire l'aggiornamento completo di ciascun server **prima** di procedere con il server successivo. Un aggiornamento completo include l'esecuzione del programma di installazione di SQL Server per aggiornare i file di programma di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , quindi azioni di aggiornamento di SharePoint per la configurazione dei servizi aggiornati. La disponibilità dei server sarà limitata finché non verranno eseguite le azioni di aggiornamento nello strumento di configurazione PowerPivot appropriato o in Windows PowerShell.  
  
-   Le versioni di tutte le istanze del Servizio di sistema PowerPivot e Analysis Services in una farm SharePoint 2010 devono essere uguali. Per informazioni su come verificare la versione, vedere la sezione [Verify the versions of PowerPivot Components and Services](#bkmk_verify_versions) in questo argomento.  
  
-   Gli strumenti di configurazione PowerPivot sono una delle funzionalità condivise di SQL Server. Tutte le funzionalità condivise vengono aggiornate contemporaneamente. Se durante un processo di aggiornamento si selezionano altre istanze o funzionalità di SQL Server per le quali è richiesto un aggiornamento della funzionalità condivisa, verrà aggiornato anche lo strumento di configurazione PowerPivot. È possibile che si riscontrino problemi se lo strumento di configurazione PowerPivot viene aggiornato ma non l'istanza di PowerPivot. Per ulteriori informazioni sulle funzionalità condivise di SQL Server, vedere [eseguire l'aggiornamento a SQL Server 2014 mediante &#40;l'&#41;installazione guidata di](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   Il componente aggiuntivo PowerPivot per SharePoint (**spspPowerPivot. msi**) viene installato side-by-side con le versioni precedenti. Ad esempio, il componente aggiuntivo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene installato nella cartella `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`.  
  

  
##  <a name="bkmk_prereq"></a> Prerequisites  
 **Permissions**  
  
-   Per aggiornare un'installazione di PowerPivot per SharePoint, è necessario essere un amministratore di farm. Per eseguire il programma di installazione di SQL Server, è necessario essere un amministratore locale.  
  
-   È necessario avere autorizzazioni **db_owner** per il database di configurazione della farm.  
  
 **SQL Server:**  
  
-   Se l'installazione di PowerPivot esistente è [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], è necessario [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Service Pack 2 (SP2) per l'aggiornamento [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
-   Se l'installazione di PowerPivot esistente è [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], è necessario [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (SP1) per l'aggiornamento [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
 **SharePoint 2010:**  
  
-   Se l'installazione esistente esegue SharePoint 2010, installare SharePoint 2010 Service Pack 2 prima di effettuare l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Per ulteriori informazioni, vedere [Service Pack 2 per Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672). Utilizzare il comando `(Get-SPfarm).BuildVersion.ToString()` di PowerShell per verificare la versione. Per correlare la versione di build alla data di rilascio, vedere [Numeri di build di SharePoint 2010](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224).  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2013"></a> Aggiornare una farm SharePoint 2013 esistente  
 Per aggiornare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] distribuito in SharePoint 2013, effettuare le operazioni seguenti:  
  
 ![aggiornamento di PowerPivot per SharePoint 2013](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "aggiornamento di PowerPivot per SharePoint 2013")  
  
1.  Eseguire il programma di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nei server back-end che eseguono [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Se il server ospita più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], aggiornare almeno l'istanza di **POWERPIVOT** . Nell'elenco seguente vengono riepilogati i passaggi dell'Installazione guidata correlati a un aggiornamento di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
    1.  Nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic su **Installazione**.  
  
    2.  Fare clic su **Aggiorna da SQL Server**.  
  
    3.  Nella pagina **Seleziona istanza** selezionare il nome dell'istanza di **POWERPIVOT** , quindi fare clic su **Avanti**.  
  
    4.  Per ulteriori informazioni, vedere [eseguire l'aggiornamento a SQL Server 2014 utilizzando l' &#40;installazione&#41; guidata](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
2.  Riavviare il server.  
  
3.  Eseguire il componente aggiuntivo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint (**spPowerPivot.msi**) in ogni server nella farm SharePoint 2013 per installare i provider di dati. Fanno eccezione i server in cui è stata eseguita l'Installazione guidata di SQL Server, che aggiorna anche i provider di dati. Per ulteriori informazioni, vedere [installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  
  
4.  **Eseguire lo strumento di configurazione PowerPivot per SharePoint 2013** in uno dei server applicazioni SharePoint per configurare la farm di SharePoint con i file di soluzione aggiornati in cui è installato il componente aggiuntivo. Non è possibile utilizzare Amministrazione centrale SharePoint per questo passaggio. Per ulteriori informazioni, vedere quanto segue:  
  
    1.  Nella pagina iniziale di Windows digitare **PowerPivot** e nei risultati della ricerca fare clic su **PowerPivot per SharePoint 2013 Configuration**. Si noti che la ricerca può restituire entrambe le versioni dello strumento di configurazione.  
  
         ![due strumenti configurazione PowerPivot](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "due strumenti configurazione PowerPivot")  
  
         e  
  
         Dal menu **Start** scegliere **tutti i programmi**, fare clic su [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], fare clic su **strumenti di configurazione**e quindi fare clic su **PowerPivot per SharePoint configurazione 2013**. Si noti che lo strumento è elencato solo se [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è installato nel server locale.  
  
    2.  All'avvio, tramite lo strumento di configurazione viene controllato lo stato dell'aggiornamento della soluzione farm PowerPivot e delle soluzioni applicazione Web PowerPivot. Se vengono rilevate versioni precedenti di queste soluzioni, verrà visualizzato il messaggio "**sono state rilevate versioni più recenti dei file di soluzione PowerPivot. Selezionare l'opzione di aggiornamento per aggiornare la farm**". Fare clic su **OK** per chiudere il messaggio di convalida del sistema.  
  
    3.  Fare clic su **Aggiorna funzionalità, servizi, applicazioni e soluzioni**, quindi fare clic su **OK**.  
  
    4.  Rivedere le azioni nell'elenco attività del riquadro sinistro ed escludere quelle che non si desidera vengano eseguite dallo strumento. Tutte le azioni sono incluse per impostazione predefinita. Per rimuovere un'azione, selezionarla nell'elenco attività di sinistra, quindi deselezionare la casella di controllo **Includere l'azione nell'elenco attività** nella pagina **Parametri** .  
  
    5.  È possibile esaminare le informazioni dettagliate nella scheda **Script** o **Output** .  
  
         Nella scheda Output viene fornito un riepilogo delle azioni che saranno eseguite dallo strumento. Queste informazioni vengono salvate in file di log nel percorso: `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`.  
  
         Nella scheda Script sono visualizzati i cmdlet di PowerShell o i riferimenti ai file di script di PowerShell che verranno eseguiti dallo strumento.  
  
    6.  Fare clic su **Convalida** per controllare la validità di ogni azione. Se **Convalida** non è disponibile, significa che tutte le azioni sono valide per il sistema. Se **Convalida** è disponibile, potrebbe essere stato modificato un valore di input (ad esempio il nome applicazione del servizio di Excel) o lo strumento potrebbe aver determinato che non è possibile eseguire una determinata azione. Se non è possibile eseguire un'azione, è necessario escluderla o correggere le condizioni sottostanti per le quali l'azione viene contrassegnata come non valida.  
  
        > [!IMPORTANT]  
        >  È necessario elaborare sempre per prima la prima azione **Aggiornare la soluzione farm**. Con questa azione verranno registrati i cmdlet di PowerShell utilizzati per configurare il server. Se viene generato un errore per questa azione, non continuare. Utilizzare invece le informazioni fornite dall'errore per diagnosticare e risolvere il problema prima di elaborare ulteriori azioni nell'elenco attività.  
  
    7.  Fare clic su **Esegui** per eseguire tutte le azioni valide per questa attività. L'opzione**Esegui** è disponibile solo dopo il superamento del controllo di convalida. Quando si fa clic su **Esegui**, viene visualizzato l'avviso seguente in cui si ricorda che le azioni vengono elaborate in modalità batch: "**tutte le impostazioni di configurazione contrassegnate come valide nello strumento verranno applicate alla farm di SharePoint. Continuare?** ".  
  
    8.  Per continuare, scegliere **Sì** .  
  
    9. Il completamento dell'aggiornamento delle soluzioni e delle funzionalità nella farm può richiedere diversi minuti. Durante questo periodo di tempo, le richieste di connessione ai dati PowerPivot **avranno esito negativo** con errori simili a "**Impossibile aggiornare i dati**" o "**si è verificato un errore durante il tentativo di eseguire l'azione richiesta. Riprovare**". Al termine dell'aggiornamento, il server diventerà disponibile e questi errori non si verificheranno più.  
  
     Per ulteriori informazioni, vedere quanto segue:  
  
    -   [Strumenti di configurazione PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools)  
  
    -   [Configurare o ripristinare PowerPivot per SharePoint strumento &#40;di configurazione PowerPivot 2013&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013)  
  
    -   [Configurazione di PowerPivot tramite Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)  
  
    -   [Informazioni di riferimento su PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  Verificare che l'aggiornamento sia stato completato correttamente eseguendo i passaggi di post-aggiornamento e controllando la versione dei server PowerPivot nella farm. Per altre informazioni, vedere [Attività di verifica post-aggiornamento](#verify) in questo argomento e la sezione seguente.  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2010"></a> Aggiornare una farm SharePoint 2010 esistente  
 Per aggiornare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] distribuito in SharePoint 2010, effettuare le operazioni seguenti:  
  
 ![aggiornamento di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "aggiornamento di PowerPivot per SharePoint 2010")  
  
1.  Scaricare [Service Pack 2 per Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672) e applicarlo a tutti i server nella farm. Verificare che l'installazione di SharePoint SP2 sia completata. Nella pagina Aggiornamento e migrazione di Amministrazione centrale aprire la pagina Controlla stato installazione prodotti e patch per visualizzare i messaggi di stato correlati a SP2.  
  
2.  Verificare che il servizio Windows Amministrazione SharePoint 2010 sia in esecuzione.  
  
    ```powershell
    Get-Service | Where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  Verificare che i servizi **sharepoint** **SQL Server Analysis Services** e **SQL Server servizio di sistema PowerPivot** vengano avviati in Amministrazione centrale SharePoint o utilizzare il comando di PowerShell seguente:.  
  
    ```powershell
    Get-SPServiceInstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  Verificare che il servizio **Windows** **SQL Server Analysis Services (PowerPivot)** sia in esecuzione.  
  
    ```powershell
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **Eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installazione** nel primo server applicazioni di SharePoint in cui viene eseguito il servizio Windows **SQL Server Analysis Services (PowerPivot)** per aggiornare l'istanza di PowerPivot. Nella pagina Installazione dell'Installazione guidata di SQL Server scegliere l'opzione di aggiornamento. Per ulteriori informazioni, vedere [eseguire l'aggiornamento a SQL Server 2014 utilizzando l' &#40;installazione&#41;guidata](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
6.  **Riavviare il server** prima di eseguire lo strumento di configurazione. Ciò garantisce che qualsiasi aggiornamento o prerequisito installato dal programma di installazione di SQL Server sia configurato completamente nel sistema.  
  
7.  **Eseguire lo strumento di configurazione PowerPivot** sul primo server applicazioni SharePoint in cui viene eseguito il servizio SQL Server Analysis Services (PowerPivot) per aggiornare le soluzioni e i servizi Web in SharePoint. Non è possibile utilizzare Amministrazione centrale per questo passaggio.  
  
    1.  Fare clic sul pulsante **Start** , scegliere **tutti i programmi**, fare clic su [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **strumenti di configurazione**e quindi su **strumento di configurazione PowerPivot**. Si noti che lo strumento è elencato solo se [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è installato nel server locale.  
  
    2.  All'avvio, tramite lo strumento di configurazione viene controllato lo stato dell'aggiornamento della soluzione farm PowerPivot e delle soluzioni applicazione Web PowerPivot. Se vengono rilevate versioni precedenti di queste soluzioni, verrà visualizzato il messaggio "sono state rilevate versioni più recenti dei file di soluzione PowerPivot. Selezionare l'opzione di aggiornamento per aggiornare la farm". Fare clic su **OK** per chiudere la finestra di messaggio.  
  
    3.  Fare clic su **Aggiorna funzionalità, servizi, applicazioni e soluzioni**, quindi su **OK** per continuare.  
  
    4.  Viene visualizzato l'avviso seguente: "le cartelle di lavoro nel dashboard di gestione PowerPivot stanno per essere aggiornate alla versione più recente. Tutte le personalizzazioni apportate alle cartelle di lavoro esistenti andranno perse. Continuare?"  
  
         Questo avviso fa riferimento alle cartelle di lavoro nel dashboard di gestione PowerPivot che generano report relativi all'attività di aggiornamento dati. Se le cartelle di lavoro sono state personalizzate, qualsiasi modifica apportata a tali cartelle di lavoro verrà persa quando i file esistenti vengono sostituiti con le versioni più recenti.  
  
         Fare clic su **Sì** per sovrascrivere le cartelle di lavoro con versioni più recenti. In alternativa, fare clic su **No** per tornare alla home page. Salvare le cartelle di lavoro in un percorso diverso in modo da conservarne una copia, quindi tornare a questo passaggio quando è possibile continuare.  
  
         Per ulteriori informazioni sulla personalizzazione delle cartelle di lavoro utilizzate nel dashboard, vedere [personalizzazione del dashboard di gestione PowerPivot](https://go.microsoft.com/fwlink/?linkID=229639).  
  
    5.  Rivedere le azioni nell'elenco attività ed escludere quelle che non si desidera vengano eseguite dallo strumento. Tutte le azioni sono incluse per impostazione predefinita. Per rimuovere un'azione, selezionarla nell'elenco attività, quindi deselezionare la casella di controllo **Includere l'azione nell'elenco attività** nella pagina Parametri.  
  
    6.  È possibile esaminare le informazioni dettagliate nella scheda **Output** o **Script** .  
  
         Nella scheda Output viene fornito un riepilogo delle azioni che saranno eseguite dallo strumento. Queste informazioni vengono salvate in file di log nel percorso: `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`.  
  
         Nella scheda Script sono visualizzati i cmdlet di PowerShell o i riferimenti ai file di script di PowerShell che verranno eseguiti dallo strumento.  
  
    7.  Fare clic su **Convalida** per controllare la validità di ogni azione. Se **Convalida** non è disponibile, significa che tutte le azioni sono valide per il sistema. Se **Convalida** è disponibile, potrebbe essere stato modificato un valore di input (ad esempio il nome applicazione del servizio di Excel) o lo strumento potrebbe aver determinato che non è possibile eseguire una determinata azione. Se non è possibile eseguire un'azione, è necessario escluderla o correggere le condizioni sottostanti per le quali l'azione viene contrassegnata come non valida.  
  
        > [!IMPORTANT]  
        >  È necessario elaborare sempre per prima la prima azione **Aggiornare la soluzione farm**. Con questa azione verranno registrati i cmdlet di PowerShell utilizzati per configurare il server. Se viene generato un errore per questa azione, non continuare. Utilizzare invece le informazioni fornite dall'errore per diagnosticare e risolvere il problema prima di elaborare ulteriori azioni nell'elenco attività.  
  
    8.  Fare clic su **Esegui** per eseguire tutte le azioni valide per questa attività. L'opzione**Esegui** è disponibile solo dopo il superamento del controllo di convalida. Quando si fa clic su **Esegui** viene visualizzato l'avviso seguente, che indica che le azioni vengono elaborate in modalità batch: "Tutte le impostazioni di configurazione contrassegnate come valide nello strumento verranno applicate alla farm di SharePoint. Continuare?"  
  
    9. Per continuare, scegliere **Sì** .  
  
    10. Il completamento dell'aggiornamento delle soluzioni e delle funzionalità nella farm può richiedere diversi minuti. Durante questo periodo di tempo, le richieste di connessione ai dati PowerPivot avranno esito negativo con errori di tipo "Impossibile aggiornare i dati" o "errore durante il tentativo di eseguire l'azione richiesta. Riprovare". Al termine dell'aggiornamento, il server diventerà disponibile e questi errori non si verificheranno più.  
  
8.  **Ripetere il processo** per ogni servizio SQL Server Analysis Services (PowerPivot) nella farm: 1) eseguire SQL Server installazione 2) eseguire lo strumento di configurazione PowerPivot.  
  
9. Verificare che l'aggiornamento sia stato completato correttamente eseguendo i passaggi di post-aggiornamento e controllando la versione dei server PowerPivot nella farm. Per altre informazioni, vedere [Attività di verifica post-aggiornamento](#verify) in questo argomento e la sezione seguente.  
  
10. **Risoluzione degli errori**  
  
     È possibile visualizzare informazioni sull'errore nel riquadro Parametri per ciascuna azione.  
  
     Per i problemi correlati alla distribuzione o al ritiro della soluzione, verificare che il servizio SharePoint 2010 Administrator sia avviato. Tramite questo servizio vengono eseguiti i processi timer che attivano le modifiche della configurazione in una farm. Se il servizio non è in esecuzione, la distribuzione o il ritiro della soluzione avrà esito negativo. Gli errori persistenti indicano che un processo di distribuzione o ritiro esistente è già in coda e blocca ulteriori azioni da parte dello strumento di configurazione.  
  
    1.  Avviare la shell di gestione SharePoint 2010 come amministratore, quindi eseguire il comando indicato di seguito per visualizzare i processi in coda:  
  
        ```cmd
        stsadm -o enumdeployments  
        ```  
  
    2.  Esaminare le distribuzioni esistenti cercando le informazioni seguenti: **Tipo** è Retraction o Deployment, **File** è powerpivotwebapp.wsp o powerpivotfarm.wsp.  
  
    3.  Per le distribuzioni o i ritiri correlati alle soluzioni PowerPivot, copiare il valore GUID per **JobID** , quindi incollarlo nel comando seguente (usare i comandi contrassegna, copia e incolla del menu modifica della Shell per copiare il GUID):  
  
        ```cmd
        stsadm -o canceldeployment -id "<GUID>"  
        ```  
  
    4.  Riprovare l'attività nello strumento di configurazione facendo clic su **Convalida** , quindi su **Esegui**.  
  
     Per tutti gli altri errori, controllare i log ULS. Per ulteriori informazioni, vedere [configurare e visualizzare i file di log di SharePoint &#40;e&#41;la registrazione diagnostica PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging).  
  

  
##  <a name="bkmk_workbooks"></a> Cartelle di lavoro  
 L'aggiornamento di un server non comporta necessariamente l'aggiornamento delle cartelle di lavoro di PowerPivot eseguite in esso, ma le cartelle di lavoro meno recenti create con la versione precedente di PowerPivot per Excel continueranno a funzionare come prima, utilizzando le funzionalità disponibili in questa versione. Le cartelle di lavoro rimangono funzionali perché in un server aggiornato è disponibile la versione del provider OLE DB di Analysis Services che faceva parte dell'installazione precedente.  
  
  
  
##  <a name="bkmk_datarefresh"></a> Aggiornamento dei dati  
 L'aggiornamento interesserà le operazioni di aggiornamento dati. L'aggiornamento dati pianificato nel server è disponibile solo per le cartelle di lavoro corrispondenti alla versione del server. Se vengono ospitate cartelle di lavoro della versione precedente, l'aggiornamento dati potrebbe non funzionare più per tali cartelle di lavoro. Per abilitare di nuovo l'aggiornamento dati, è necessario aggiornare le cartelle di lavoro. È possibile aggiornare ogni cartella di lavoro manualmente in PowerPivot per Excel o abilitare la funzionalità di aggiornamento automatico dei dati in SharePoint 2010. Con l'aggiornamento automatico sarà possibile aggiornare una cartella di lavoro alla versione corrente prima dell'esecuzione dell'aggiornamento dati, consentendo alle operazioni di aggiornamento dati di rimanere pianificate.  
  

  
##  <a name="bkmk_verify_versions"></a>Verificare le versioni dei componenti e dei servizi PowerPivot  
 La versione di tutte le istanze del servizio di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e di Analysis Services deve essere uguale. Per verificare che la versione di tutti i componenti server sia uguale, controllare le informazioni sulla versione per gli elementi seguenti:  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>Verificare la versione delle soluzioni PowerPivot e del Servizio di sistema PowerPivot  
 Eseguire il comando PowerShell seguente:  
  
```powershell
Get-PowerPivotSystemService  
```  
  
 Verificare **CurrentSolutionVersion**. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è la versione 12,0. \<major > di compilazione. \<minor compilazione >  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>Verificare la versione del servizio Windows Analysis Services  
 Se sono stati aggiornati solo alcuni dei server [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] di una farm SharePoint 2010, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nei server non aggiornati sarà meno recente della versione prevista nella farm. Sarà necessario effettuare l'aggiornamento di tutti i server alla stessa versione affinché possano essere utilizzati. Utilizzare uno dei metodi seguenti per verificare la versione del servizio Windows SQL Server Analysis Services (PowerPivot) in ogni computer.  
  
 **Esplora file di Windows**:  
  
1.  Passare alla cartella **Bin** per l'istanza di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Ad esempio `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`.  
  
2.  Fare clic con il pulsante destro del mouse su `msmdsrv.exe`e selezionare **Proprietà**.  
  
3.  Scegliere **Dettagli**.  
  
4.  la versione del file di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] deve essere 12,00. \<major > di compilazione. \<minor > di compilazione.  
  
5.  Verificare che il numero sia identico alla versione della soluzione e del Servizio di sistema PowerPivot.  
  
 **Informazioni sull'avvio del servizio:**  
  
 All'avvio, il servizio PowerPivot scrive le informazioni sulla versione nel registro eventi di Windows.  
  
1.  Eseguire il `eventvwr`  
  
2.  Creare un filtro per l'elemento `MSOLAP$POWERPIVOT`di origine.  
  
3.  Cercare un evento del livello informazioni simile al seguente  
  
     Servizio   avviato. Microsoft SQL Server Analysis Services 64 bit Evaluation (x64) RTM **12.0.2000.8**.  
  
 **Utilizzare PowerShell per verificare la versione del file.**  
  
 È possibile utilizzare PowerShell per verificare la versione del prodotto. PowerShell è un'ottima scelta se si desidera eseguire lo script o automatizzare la verifica della versione.  
  
```powershell
(Get-ChildItem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 Il comando PowerShell riportato sopra restituisce informazioni simili alle seguenti:  
  
 VersioneProdotto   VersioneFile           NomeFile  
  
 **12.0.2000.8** 2014.0120.200 C:\Programmi\Microsoft SQL Server\MSAS12. POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>Verificare la versione del provider di dati MSOLAP in SharePoint  
 Utilizzare le istruzioni seguenti per controllare quali versioni dei provider OLE DB di Analysis Services sono considerate attendibili da Excel Services. È necessario essere amministratore di una farm o di un'applicazione di servizio per controllare le impostazioni del provider di dati attendibile di Excel Services.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione di servizio Excel Services, ad esempio **ExcelServiceApp1**.  
  
3.  Fare clic su **Provider di dati attendibili**. Dovrebbe essere visualizzato MSOLAP.5 (Provider OLE DB Microsoft per OLAP Services 11.0). Se è stata aggiornata l'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , sarà anche visualizzato MSOLAP.4 dalla versione precedente.  
  
4.  Per ulteriori informazioni, vedere [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services).  
  
 MSOLAP.4 viene descritto come provider Microsoft OLE DB per OLAP Services 10.0. Questa versione potrebbe essere quella predefinita per [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] installata con Excel Services o la versione per [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] . La versione predefinita installata da SharePoint non supporta l'accesso ai dati PowerPivot. È necessario disporre della versione per [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o successiva per connettersi alle cartelle di lavoro di PowerPivot su SharePoint. Per verificare la disponibilità della versione per [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , utilizzare le istruzioni nella sezione precedente in cui viene illustrato come verificare la versione visualizzando le proprietà del file.  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>Verificare la versione del provider di dati ADOMD.NET  
 Utilizzare le istruzioni seguenti per controllare quale versione di ADOMD.NET è installata. È necessario essere amministratore di una farm o di un'applicazione di servizio per controllare le impostazioni del provider di dati attendibile di Excel Services.  
  
1.  Nel server applicazioni SharePoint, passare a `c:\Windows\Assembly`.  
  
2.  Ordinare per nome di assembly e individuare **Microsoft.Analysis Services.Adomd.Client**.  
  
3.  Verificare di avere la versione 12,0. numero \<build >.  
  

##  <a name="geminifarm"></a>Aggiornamento di più server PowerPivot per SharePoint in una farm di SharePoint  
 In una topologia multiserver in cui sono inclusi più server [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , la versione di tutti i componenti e di tutte le istanze del server deve essere uguale. Il server che esegue la versione più recente del software imposta il livello per tutti i server nella farm. Se vengono aggiornati solo alcuni server, quelli che eseguono versioni meno recenti del software non saranno più disponibili finché non verranno aggiornati.  
  
 Dopo l'aggiornamento del primo server, gli altri server che non sono ancora stati aggiornati **non saranno più disponibili**. La disponibilità viene ripristinata quando tutti i server presentano lo stesso livello funzionale.  
  
 Con il programma di installazione di SQL Server vengono aggiornati i file di soluzione PowerPivot nel computer fisico, ma per aggiornare le soluzioni utilizzate nella farm, è necessario utilizzare lo strumento di configurazione PowerPivot descritto in una sezione precedente di questo argomento.  

##  <a name="qfe"></a>Applicazione di un QFE a un'istanza PowerPivot nella farm  
 L'applicazione della patch a un server PowerPivot per SharePoint consente di effettuare l'aggiornamento dei file di programma esistenti a una versione più recente in cui è inclusa una correzione per un problema specifico. In caso di applicazione di una correzione QFE a una topologia multiserver, non esiste un server primario da cui iniziare. È possibile iniziare con qualsiasi server finché si applica la stessa correzione QFE agli altri server PowerPivot nella farm.  
  
 Quando si applica la correzione QFE, è necessario eseguire anche un passaggio di configurazione per aggiornare le informazioni sulla versione del server nel database di configurazione della farm. La versione del server per cui è stata installata la patch diventa la nuova versione prevista per la farm. Fino a quando la correzione QFE non viene applicata e configurata in tutti i computer, le istanze di PowerPivot per SharePoint che non contengono la correzione QFE non saranno disponibili per gestire le richieste per i dati PowerPivot.  
  
 Per verificare che la correzione QFE sia stata applicata e configurata correttamente, seguire queste istruzioni:  
  
1.  Installare la patch attenendosi alle istruzioni fornite con la correzione QFE.  
  
2.  Avviare lo strumento di configurazione PowerPivot.  
  
3.  Fare clic su **Aggiorna funzionalità, servizi, applicazioni e soluzioni**, quindi fare clic su **OK**.  
  
4.  Rivedere le azioni incluse nell'attività di aggiornamento, quindi fare clic su **Convalida**.  
  
5.  Fare clic su **Esegui** per applicare le azioni.  
  
6.  Ripetere per le istanze di PowerPivot per SharePoint aggiuntive nella farm.  
  
    > [!IMPORTANT]  
    >  In una distribuzione multiserver assicurarsi di applicare la patch a ogni istanza e di configurarla prima di continuare con il computer successivo. È necessario completare l'attività di aggiornamento con lo strumento di configurazione PowerPivot per l'istanza corrente prima di passare all'istanza successiva.  
  
 Per controllare le informazioni sulla versione per i servizi della farm, utilizzare la pagina **Controlla stato installazione prodotti e patch** nella sezione Gestione aggiornamento e patch di Amministrazione centrale.  
  
##  <a name="verify"></a> Attività di verifica post-aggiornamento  
 Al termine dell'aggiornamento, eseguire i passaggi seguenti per verificare che il server sia operativo.  
  
|Attività|Collegamento|  
|----------|----------|  
|Verificare che il servizio sia in esecuzione in tutti i computer in cui è eseguito PowerPivot per SharePoint.|[Avviare o arrestare un server PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server)|  
|Verificare l'attivazione della funzionalità a livello di raccolta siti.|[Attivare l'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)|  
|Verificare che le singole cartelle di lavoro di PowerPivot vengano caricate correttamente aprendo una cartella di lavoro e facendo clic sui filtri e sul filtro dei dati per avviare una query.|Verificare la presenza di file memorizzati nella cache sul disco rigido. Un file memorizzato nella cache conferma che il file di dati è stato caricato in quel server fisico. Cercare i file memorizzati nella cache nella cartella c:\Programmi\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup.|  
|Testare l'aggiornamento dei dati nelle cartelle di lavoro selezionate configurate per l'aggiornamento dei dati.|Il modo più semplice per testare l'aggiornamento dei dati consiste nel modificare una pianificazione di aggiornamento dei dati, scegliendo la casella di controllo **Aggiorna anche appena possibile** in modo che l'aggiornamento dei dati venga eseguito immediatamente. Con questo passaggio si determinerà se l'aggiornamento dei dati viene completato correttamente per la cartella di lavoro corrente. Ripetere questi passaggi per le altre cartelle di lavoro utilizzate frequentemente per assicurare che l'aggiornamento dei dati sia operativo. Per ulteriori informazioni sulla pianificazione dell'aggiornamento dei dati, vedere [pianificare un aggiornamento &#40;dati&#41;PowerPivot per SharePoint](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md).|  
|Nel tempo, monitorare report dell'aggiornamento dati in Dashboard di gestione PowerPivot per verificare che non ci siano errori di aggiornamento dati.|[Dati di utilizzo e dashboard di gestione PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)|  
  
 Per ulteriori informazioni su come configurare le impostazioni e le funzionalità di PowerPivot, vedere [amministrazione e configurazione del server PowerPivot in Amministrazione centrale](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
 Per istruzioni dettagliate che consentono di eseguire tutte le attività di configurazione post-installazione, vedere [ &#40;configurazione iniziale PowerPivot per SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  

## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)    
 [Installazione di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
