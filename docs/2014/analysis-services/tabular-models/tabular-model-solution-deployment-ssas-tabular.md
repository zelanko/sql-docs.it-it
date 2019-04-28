---
title: Distribuzione di soluzioni di modelli tabulari (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: aff96558-e5e5-4b95-8ddf-ee0709c842fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01f4bcc06ca7bf8bcee3cf581ad0c2bec3ba4f9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794605"
---
# <a name="tabular-model-solution-deployment-ssas-tabular"></a>Distribuzione di una soluzione del modello tabulare (SSAS tabulare)
  Una volta creato, un progetto di modello tabulare deve essere distribuito affinché gli utenti esplorino il modello tramite un'applicazione client di creazione report. In questo argomento vengono illustrate le varie proprietà e i diversi metodi che è possibile utilizzare in caso di distribuzione di soluzioni di modelli tabulari nell'ambiente.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Distribuzione di un modello tabulare da SQL Server Data Tools (SSDT)](#bkmk_deploying_bism)  
  
-   [Proprietà della distribuzione](#bkmk_deploy_props)  
  
-   [Metodi di distribuzione](#bkmk_meth)  
  
-   [Configurazione del server di distribuzione e connessione a un modello distribuito](#bkmk_connecting)  
  
-   [Attività correlate](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 La distribuzione di un modello tabulare consente di creare un database modello in un ambiente di testing, di gestione temporanea e di produzione. Gli utenti possono quindi connettersi al modello distribuito tramite un file di connessione con estensione bism in Sharepoint o utilizzando una connessione dati direttamente dalle applicazioni client di creazione report quali Microsoft Excel, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]o un'applicazione personalizzata. Il database dell'area di lavoro del modello, generato quando si crea un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e usato per creare il modello rimarrà nell'istanza del server dell'area di lavoro consentendo di apportare modifiche al progetto del modello e di eseguire nuovamente la distribuzione nell'ambiente di testing, di gestione temporanea o di produzione quando necessario.  
  
##  <a name="bkmk_deploying_bism"></a> Distribuzione di un modello tabulare da SQL Server Data Tools (SSDT)  
 La distribuzione è un processo semplice, tuttavia, è necessario effettuare alcuni passaggi per assicurarsi che il modello venga distribuito nell'istanza di Analysis Services corretta e con le opzioni di configurazione appropriate.  
  
 I modelli tabulari sono definiti con diverse proprietà di distribuzione specifiche. Quando si esegue una distribuzione, viene stabilita una connessione all'istanza di Analysis Services specificata nella proprietà **Server** . Viene quindi creato un nuovo database modello con il nome specificato nella proprietà **Database** , se non ne esiste già uno. I metadati dal file Model. bim del progetto di modello viene utilizzato per configurare gli oggetti nel database modello sul server di distribuzione. Con **Opzione di elaborazione**è possibile specificare se vengono distribuiti solo i metadati del modello, creando il database modello. Se invece viene specificata l'opzione **Predefinita** o **Completa** , le credenziali di rappresentazione usate per connettersi alle origini dati vengono passate in memoria dal database dell'area di lavoro modello al database modello distribuito. Tramite Analysis Services viene quindi eseguita l'elaborazione per il popolamento di dati nel modello distribuito. Una volta completato il processo di distribuzione, il modello può essere connesso tramite applicazioni client utilizzando una connessione dati o tramite un file di connessione con estensione bism in SharePoint.  
  
##  <a name="bkmk_deploy_props"></a> Proprietà della distribuzione  
 Le proprietà di Opzioni di distribuzione e di Server di distribuzione del progetto consentono di specificare la modalità di distribuzione di un modello e la relativa posizione in un ambiente di gestione temporanea o di produzione di Analysis Services. Anche se le impostazioni delle proprietà predefinite vengono definite per tutti i progetti di modello, a seconda dei requisiti di distribuzione specifici è possibile modificare le impostazioni di queste proprietà per ogni progetto. Per altre informazioni sull'impostazione delle proprietà di distribuzione predefinite, vedere [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](properties-ssas-tabular.md).  
  
### <a name="deployment-options-properties"></a>Proprietà di Opzioni di distribuzione  
 Tra le proprietà di Opzioni di distribuzione sono incluse le seguenti:  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Opzione di elaborazione**|**Default**|Questa proprietà consente di specificare il tipo di elaborazione necessario quando vengono distribuite le modifiche agli oggetti. Per questa proprietà sono disponibili le opzioni seguenti:<br /><br /> **Default** -questa impostazione specifica di Analysis Services verrà stabilito il tipo di elaborazione necessario. Gli oggetti non elaborati verranno elaborati e, se necessario, verranno ricalcolate le relazioni tra attributi, le gerarchie degli attributi e degli utenti e le colonne calcolate. Questa impostazione comporta in genere una durata inferiore della distribuzione rispetto all'utilizzo dell'opzione di elaborazione completa.<br /><br /> **Non elaborare** -questa impostazione specifica verranno distribuiti solo i metadati. Dopo aver effettuato la distribuzione, potrebbe essere necessario eseguire un'operazione di elaborazione nel modello distribuito per aggiornare e ricalcolare i dati.<br /><br /> **Completa** -questa impostazione specifica che sia i metadati vengono distribuiti e viene eseguita un'operazione completa. In questo modo, il modello distribuito dispone degli aggiornamenti più recenti sia per i metadati sia per i dati.|  
|**Distribuzione transazionale**|**False**|Questa proprietà consente di specificare se la distribuzione è transazionale. Per impostazione predefinita, la distribuzione di tutti gli oggetti o di quelli modificati non è transazionale con l'elaborazione di tali oggetti distribuiti. La distribuzione può avere esito positivo ed essere persistente anche in caso di esito negativo dell'elaborazione. Questa impostazione può essere modificata in modo da incorporare la distribuzione e l'elaborazione in una singola transazione.|  
|**Modalità query**|**In-Memory**|Questa proprietà consente di specificare che l'origine dalla quale vengono restituiti i risultati della query è in esecuzione in modalità In memoria (memorizzazione nella cache) o DirectQuery. Per questa proprietà sono disponibili le opzioni seguenti:<br /><br /> **DirectQuery** -specifica tutte le query sul modello devono utilizzare solo l'origine dati relazionale.<br /><br /> **DirectQuery con In memoria** : specifica che, per impostazione predefinita, le risposte alle query verranno fornite usando l'origine relazionale, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> **In memoria** : specifica che le risposte alle query verranno fornite usando solo la cache.<br /><br /> **In memoria con DirectQuery** : specifica che, per impostazione predefinita, le risposte alle query verranno fornite utilizzando la cache, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> <br /><br /> Per altre informazioni, vedere [Modalità DirectQuery &#40;SSAS tabulare&#41;](directquery-mode-ssas-tabular.md).|  
  
### <a name="deployment-server-properties"></a>Proprietà di Server di distribuzione  
 Tra le proprietà di Server di distribuzione sono incluse le seguenti:  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Server**<br /><br /> Viene impostata quando si crea il progetto.|**localhost**|Questa proprietà, impostata quando si crea il progetto, consente di specificare il nome dell'istanza di Analysis Services in cui verrà distribuito il modello. Per impostazione predefinita, il modello sarà distribuito nell'istanza predefinita di Analysis Services nel computer locale. Tuttavia, questa impostazione può essere modificata per specificare un'istanza denominata nel computer locale oppure qualsiasi istanza in un computer remoto per cui si dispone dell'autorizzazione necessaria per creare oggetti di Analysis Services.|  
|**Edizione**|Stessa edizione dell'istanza in cui si trova il server dell'area di lavoro.|Questa proprietà consente di specificare l'edizione del server Analysis Services in cui verrà distribuito il modello. L'edizione del server consente di definire le varie funzionalità che possono essere incorporate nel progetto. Per impostazione predefinita, l'edizione sarà quella del server Analysis Services locale. Se si specifica un server Analysis Services diverso, ad esempio, un server Analysis Services di produzione, assicurarsi di specificare l'edizione di tale server.|  
|**Database**|**\<projectname>**|Questa proprietà consente di specificare il nome del database di Analysis Services in cui verrà creata un'istanza degli oggetti modello durante la distribuzione. Questo nome verrà specificato anche nella connessione dati di uno strumento client di creazione report o in un file di connessione dati con estensione bism.<br /><br /> È possibile modificare questo nome in qualsiasi momento durante la creazione del modello. Se si modifica il nome dopo la distribuzione del modello, le modifiche apportate dopo questa operazione non verranno applicate al modello distribuito in precedenza. Ad esempio, se si apre una soluzione denominata `TestDB`, la si distribuisce con il nome del database modello predefinito Model, successivamente la si modifica e si assegna il nome `Sales` al database modello, nell'istanza di Analysis Services in cui sono state distribuite le soluzioni verranno visualizzati database distinti, uno denominato Model e un altro Sales.|  
|**Nome cubo**|**Modello**|Questa proprietà consente di specificare il nome del cubo come mostrato negli strumenti client (ad esempio Excel) e negli oggetti AMO (Analysis Management Objects).|  
  
### <a name="directquery-options-properties"></a>Proprietà delle opzioni DirectQuery  
 Tra le proprietà di Opzioni di distribuzione sono incluse le seguenti:  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Impostazioni di rappresentazione**|**Predefinita**|Questa proprietà consente di specificare le impostazioni di rappresentazione utilizzate in caso di connessione di un modello in esecuzione in modalità DirectQuery alle origini dati. Le credenziali di rappresentazione non vengono utilizzate in caso di esecuzione di query sulla cache in memoria. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Default** -questa impostazione specifica di Analysis Services verrà utilizzata l'opzione specificata nella pagina Impostazioni di rappresentazione durante la connessione all'origine dati è stata creata tramite l'importazione guidata tabella.<br /><br /> **ImpersonateCurrentUser** -questa impostazione specifica l'account utente dell'utente attualmente connesso verrà usata durante la connessione a tutte le origini dati.|  
  
##  <a name="bkmk_meth"></a> Metodi di distribuzione  
 Sono disponibili diversi metodi che è possibile utilizzare per distribuire un progetto di modello tabulare. La maggior parte dei metodi di distribuzione che è possibile utilizzare per altri progetti Analysis Services, ad esempio multidimensionali, possono anche essere utilizzati per distribuire progetti di modello tabulare.  
  
|Metodo|Descrizione|Collegamento|  
|------------|-----------------|----------|  
|**Comando Distribuisci in SQL Server Data Tools**|Il comando Distribuisci offre un metodo semplice e intuitivo per distribuire un progetto di modello tabulare dall'ambiente di creazione [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] .<br /><br /> **\*\* Attenzione \*\*** Questo metodo non deve essere usato per la distribuzione nei server di produzione. L'utilizzo di questo metodo può sovrascrivere alcune proprietà in un modello esistente.|[Distribuire da SQL Server Data Tools &#40;SSAS tabulare&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**Automazione AMO (Analysis Management Objects)**|AMO (Analysis Management Objects) offre un'interfaccia di programmazione per il set di comandi completo per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], inclusi comandi che possono essere utilizzati per la distribuzione della soluzione. Come approccio per la distribuzione della soluzione, l'automazione AMO (Analysis Management Objects) è la più flessibile, ma richiede anche un lavoro di programmazione.  Il vantaggio principale offerto da AMO è che consente di utilizzare SQL Server Agent insieme all'applicazione AMO per eseguire la distribuzione in base a una pianificazione predefinita.|[Sviluppo con Analysis Management Objects &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|Utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per generare uno script XMLA dei metadati di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente, quindi eseguire tale script in un altro server per ricreare il database iniziale. Per creare script XMLA in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , è sufficiente definire il processo di distribuzione e quindi codificarlo e memorizzarlo in uno script XMLA. Dopo aver salvato lo script XMLA in un file, è possibile eseguire lo script in base a una pianificazione oppure incorporarlo nello script di un'applicazione che si connette direttamente a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> È inoltre possibile eseguire script XMLA a intervalli predefiniti tramite SQL Server Agent, ma questo metodo non è caratterizzato dalla stessa flessibilità del metodo basato sull'automazione AMO. Nella libreria AMO è disponibile un'ampia gamma di funzionalità che supportano l'insieme completo di comandi amministrativi.|[Distribuire soluzioni di modelli usando XMLA](../multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**Distribuzione guidata**|Distribuzione guidata consente di utilizzare i file di output XMLA generati da un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per distribuire i metadati del progetto in un server di destinazione. Grazie alla Distribuzione guidata è possibile eseguire la distribuzione direttamente dal file di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] creato nella directory di output tramite la compilazione del progetto.<br /><br /> Il vantaggio principale rappresentato dall'utilizzo della Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è la praticità. È possibile salvare script della Distribuzione guidata nello stesso modo in cui è possibile salvare uno script XMLA per un utilizzo successivo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La Distribuzione guidata può essere eseguita sia in modalità interattiva sia dal prompt dei comandi tramite l'utilità di distribuzione.|[Deploy Model Solutions Using the Deployment Wizard](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**Utilità di distribuzione**|L'utilità di distribuzione consente di avviare il motore di distribuzione di Analysis Services da un prompt dei comandi.|[Distribuire soluzioni di modelli con l'utilità di distribuzione](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**Sincronizzazione guidata database**|Sincronizzazione guidata database consente di sincronizzare i metadati e i dati tra due database qualsiasi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> È possibile utilizzare la Sincronizzazione guidata database per copiare sia dati sia metadati da un server di origine in un server di destinazione. Se nel server di destinazione non è disponibile una copia del database che si desidera distribuire, in tale server viene copiato un nuovo database. Se invece nel database di destinazione è già inclusa una copia dello stesso database, il database nel server di destinazione viene aggiornato per utilizzare i metadati e i dati del database di origine.|[Sincronizzare database di Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)|  
|**Backup e ripristino**|Il backup rappresenta il metodo di trasferimento di database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] più semplice. Nella finestra di dialogo **Backup** è possibile definire la configurazione delle opzioni desiderate e quindi eseguire il backup dalla finestra di dialogo stessa. In alternativa, è possibile creare uno script che può essere salvato ed eseguito in base alle specifiche esigenze.<br /><br /> Il metodo Backup e ripristino non viene utilizzato con la stessa frequenza degli altri metodi, anche se consente di completare rapidamente un'operazione di distribuzione con requisiti di infrastrutture minimi.|[Backup e ripristino di database di Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_connecting"></a> Configurazione del server di distribuzione e connessione a un modello distribuito  
 Dopo la distribuzione di un modello, è possibile configurare ulteriori impostazioni relative alla sicurezza dell'accesso ai dati del modello, ai backup e alle operazioni di elaborazione sul server Analysis Services tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Anche se queste proprietà e le impostazioni di configurazione esulano dall'ambito di questo argomento, sono comunque molto importanti per garantire che i dati del modello distribuito siano protetti e tenuti aggiornati; inoltre, offrono una risorsa di analisi dati preziosa per gli utenti dell'organizzazione.  
  
 Dopo la distribuzione di un modello e la configurazione delle impostazioni del server facoltative, il modello può essere connesso da applicazioni client di creazione report e utilizzato per la visualizzazione e l'analisi dei metadati del modello. La connessione a un database modello distribuito da applicazioni client non rientra nell'ambito di questo argomento. Per ulteriori informazioni sulla connessione a un database modello da applicazioni client, vedere [Tabular Model Data Access](tabular-model-data-access.md).  
  
##  <a name="bkmk_rt"></a> Attività correlate  
  
|Attività|Descrizione|  
|----------|-----------------|  
|[Distribuire da SQL Server Data Tools &#40;SSAS tabulare&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|Viene descritto come configurare le proprietà di distribuzione e distribuire un progetto di modello tabulare tramite il comando Distribuisci in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].|  
|[Distribuire soluzioni di modelli tramite la Distribuzione guidata](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|Negli argomenti in questa sezione viene descritto come utilizzare la Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per distribuire sia soluzioni di modelli tabulari e che di modelli multidimensionali.|  
|[Distribuire soluzioni di modelli con l'utilità di distribuzione](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Viene descritto come utilizzare l'utilità di distribuzione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per distribuire sia soluzioni di modelli tabulari e che di modelli multidimensionali.|  
|[Distribuire soluzioni di modelli utilizzando XMLA](../multidimensional-models/deploy-model-solutions-using-xmla.md)|Viene descritto come utilizzare XMLA per distribuire [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] soluzioni tabulari e multidimensionali.|  
|[Sincronizzare database di Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)|Viene descritto come utilizzare la Sincronizzazione guidata database per sincronizzare i metadati e i dati tra due database tabulari o multidimensionali di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vedere anche  
 [Connettersi a un database modello tabulare &#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)  
  
  
