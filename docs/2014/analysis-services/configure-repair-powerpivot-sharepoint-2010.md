---
title: Configurare o ripristinare PowerPivot per SharePoint 2010 (strumento di configurazione PowerPivot) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d61f49c5-efaa-4455-98f2-8c293fa50046
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a80e362c97df74773d303a4b022d376fff40fb70
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360343"
---
# <a name="configure-or-repair-powerpivot-for-sharepoint-2010-powerpivot-configuration-tool"></a>Configurare o ripristinare PowerPivot per SharePoint 2010 (strumento di configurazione PowerPivot)
  Per configurare o ripristinare un'installazione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerPivot per SharePoint 2010, usare lo strumento di configurazione PowerPivot. Tramite lo strumento di configurazione viene innanzitutto analizzato il sistema, dopodiché viene restituito un elenco di azioni necessarie per completare o ripristinare l'installazione. Con l'installazione guidata [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] vengono installati lo strumento di configurazione PowerPivot per SharePoint 2010 e quello per SharePoint 2013. In questo argomento viene descritto lo strumento di configurazione PowerPivot per SharePoint 2010. Per altre informazioni su SharePoint 2010, vedere [Configura o Ripristina PowerPivot per SharePoint 2013 &#40;strumento di configurazione PowerPivot&#41;](power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md).  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 
  
##  <a name="bkmk_before"></a> Prima di iniziare  
 Lo strumento di configurazione PowerPivot per SharePoint 2010 esegue l'analisi di file di programma, impostazioni del Registro di sistema e porte disponibili. Per usare al meglio gli strumenti, vedere gli argomenti seguenti.  
  
-   Requisiti generali per eseguire lo strumento di configurazione, [PowerPivot Configuration Tools](power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
-   PowerPivot per SharePoint 2010 richiede applicazioni Web configurate per l'autenticazione in modalità classica. Se l'applicazione viene creata tramite lo strumento di configurazione di PowerPivot per SharePoint 2010, è configurata per la modalità classica.  
  
-   La porta 80 deve essere disponibile se una delle attività selezionate richiede la creazione e la configurazione di un'applicazione Web allo strumento di configurazione.  
  
##  <a name="bkmk_using"></a> Usando lo strumento di configurazione PowerPivot  
 Nella prima pagina dello strumento viene fornito un riepilogo dei valori di input usati per configurare la farm di SharePoint. Oltre ai valori di input che è necessario specificare, per configurare il sistema sono necessari dei valori predefiniti. Vengono usati nomi predefiniti per applicazioni del servizio, database di applicazioni del servizio e proprietà di applicazioni del servizio.  
  
> [!TIP]  
>  Se lo strumento di configurazione PowerPivot esegue l'analisi del computer e viene restituito un elenco di attività vuoto nel riquadro sinistro, non è necessaria la configurazione per alcuna funzionalità o impostazione. Per modificare la configurazione di PowerPivot o SharePoint, usare Windows PowerShell o le pagine di gestione in Amministrazione centrale SharePoint. Per altre informazioni, vedere [amministrazione Server PowerPivot e la configurazione in Amministrazione centrale](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 I valori per gli account del servizio sono usati per più servizi. Ad esempio, l'account predefinito viene usato dallo strumento di configurazione PowerPivot nella prima pagina per impostare tutte le identità del pool di applicazioni. È possibile cambiare questi account in un secondo momento modificando le proprietà dell'applicazione di servizio in Amministrazione centrale.  
  
-   L'eccezione a questa regola dello strumento di configurazione di PowerPivot per SharePoint 2010 è l'account del servizio Analysis Services. Questo account viene specificato durante l'installazione e si digita una password per l'account tramite il **registrare SQL Server Analysis Services (PowerPivot nel Server locale)** azione. Nella pagina di riepilogo non è incluso un campo per questa password, pertanto assicurarsi di immetterlo nella pagina di questa azione.  
  
 Lo strumento dispone di un'interfaccia a schede comprendente input di parametri, script di Windows PowerShell e messaggi di stato.  
  
 Lo strumento di configurazione PowerPivot usano Windows PowerShell per configurare il server. È possibile fare clic il **Script** pressione di tab per esaminare lo script di Windows PowerShell di.  
  
 ![Interfaccia utente dello strumento di configurazione](media/ssas-pctui.gif "interfaccia utente dello strumento di configurazione")  
  
##  <a name="bkmk_steps"></a> Passaggi di configurazione  
 Il collegamento allo strumento di configurazione è visibile solo quando PowerPivot per SharePoint 2010 è installato nel server locale.  
  
1.  Nel **avviare** dal menu **tutti i programmi**, fare clic su [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], fare clic su **strumenti di configurazione**e quindi fare clic su **dello strumento di configurazione PowerPivot** .  
  
2.  Fare clic su **Configura o ripristina PowerPivot per SharePoint**.  
  
3.  Espandere completamente la finestra. Nella parte inferiore della finestra dovrebbe essere disponibile una barra contenente i comandi **Convalida**, **Esegui**ed **Esci** .  
  
4.  **Account predefinito:** Nella scheda parametri digitare un account utente di dominio per il **nome utente Account predefinito**. L'account è usato per eseguire il provisioning di servizi essenziali, incluso il pool di applicazioni del servizio PowerPivot. Non specificare un account predefinito quale Servizio di rete o Sistema locale. Le configurazioni tramite cui vengono specificati account predefiniti vengono bloccate dallo strumento.  
  
     **Passphrase** : digitare una passphrase. Per una nuova farm di SharePoint, la passphrase viene usata ogni volta che si aggiunge un nuovo server o una nuova applicazione alla farm di SharePoint. Se si tratta di una farm esistente, immettere la passphrase che consente di aggiungere un'applicazione server alla farm.  
  
5.  **Porta:** facoltativamente, digitare un numero di porta per la connessione all'applicazione Web Amministrazione centrale oppure usare il numero generato casualmente che viene fornito. Viene verificato che il numero sia disponibile prima di fornirlo come opzione.  
  
6.  Fare clic su **registrare SQL Server Analysis Services (PowerPivot) sul Server locale**.  
  
     Immettere la password dell'account del servizio Analysis Services.  
  
7.  Facoltativamente, rivedere i valori di input rimanenti usati per completare ogni azione. Per altre informazioni su ognuno, vedere [Valori di input usati per configurare il server](#bkmk_input) in questo argomento.  
  
8.  Facoltativamente, rimuovere eventuali azioni che non si desidera elaborare. Ad esempio, se si desidera configurare il servizio di archiviazione sicura in un secondo momento, fare clic su **Configurare il servizio di archiviazione sicura**, quindi deselezionare la casella di controllo **Includere l'azione nell'elenco attività**.  
  
9. Fare clic su **Convalida** per verificare se sono disponibili informazioni sufficienti per lo strumento al fine di elaborare le azioni nell'elenco.  
  
    > [!NOTE]  
    >  Se si verifica un errore di configurazione della farm, è possibile che SharePoint 2010 Server SP1 non sia installato.  
  
10. Fare clic su **Esegui** per elaborare tutte le azioni nell'elenco attività. Il pulsante **Esegui** viene abilitato dopo avere convalidato le azioni. Se **Esegui** non è abilitato, fare clic su **Convalida** .  
  
11. [Verify a PowerPivot for SharePoint Installation](instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_input"></a> Valori di input usati per configurare il server  
 Lo strumento di configurazione PowerPivot è basato sull'utilizzo di una combinazione di valori di input da digitare e di valori predefiniti rilevati o usati automaticamente.  
  
 L'elenco delle azioni elencate nello strumento di configurazione dipende dalla configurazione corrente delle farm di SharePoint. Ad esempio, se la farm di SharePoint è già configurata, nello strumento non è elencata alcuna azione. È possibile eseguire lo strumento in qualsiasi momento per configurare, ripristinare o rilevare errori di configurazione. Se servizi necessari quali Excel Services o il servizio di archiviazione sicura non sono in esecuzione nella farm, verranno rilevati i servizi mancanti e verranno proposte le opzioni per abilitarli. Se non è necessaria alcuna azione, l'elenco attività sarà vuoto.  
  
 Nella tabella seguente vengono descritti i valori usati per configurare il server.  
  
|Pagina|Valore di input|Origine|Descrizione|  
|----------|-----------------|------------|-----------------|  
|**Configurare o ripristinare PowerPivot per SharePoint**|Account predefinito|Utente corrente|L'account predefinito è un account utente di Windows di dominio usato per eseguire il provisioning di servizi condivisi nella farm. Viene usato per eseguire il provisioning dell'applicazione del servizio PowerPivot, il servizio di archiviazione sicura, Excel Services, l'identità del pool di applicazioni Web, l'amministratore della raccolta siti e l'account di aggiornamento dati automatico PowerPivot.<br /><br /> Per impostazione predefinita, lo strumento immetto l'account di dominio dell'utente corrente. A meno che non si intenda configurare un server a scopo di valutazione, è necessario sostituirlo con un account utente di dominio diverso.<br /><br /> È inoltre possibile modificare in seguito le identità del servizio tramite Amministrazione centrale.<br /><br /> Facoltativamente, è possibile usare lo strumento di configurazione PowerPivot per specificare gli account dedicati per gli elementi seguenti:<br /><br /> applicazione Web, tramite la pagina **Creare applicazione Web predefinita** (supponendo che si stia creando un'applicazione Web per la farm).<br /><br /> PowerPivot account di aggiornamento dati automatico, tramite il **creare Account automatico per Datarefresh** pagina in questo strumento.|  
||Server di database|Istanza denominata di PowerPivot locale, se disponibile|Se un'istanza del motore di database è installata come un'istanza denominata di PowerPivot, il campo del server di database verrà popolato con questa istanza. Se il motore di database non è installato, questo campo è vuoto. È necessario fornire un'istanza. Può trattarsi di qualsiasi versione o edizione di SQL Server supportata per le farm SharePoint.|  
||Passphrase|Input dell'utente|Se si crea una nuova farm, la passphrase immessa sarà quella per la farm. Se si aggiunge PowerPivot per SharePoint a una farm esistente, è necessario fornire la passphrase definita per la farm al momento della creazione.|  
||Porta di Amministrazione centrale SharePoint|Predefinito, se necessario|Se la farm non è configurata, verranno fornite opzioni per creare la farm, incluso un endpoint HTTP per Amministrazione centrale. Per impostazione predefinita, viene usato un numero di porta generato casualmente che non è in uso.|  
|**Configurare la nuova farm**|Server di database<br /><br /> Account farm<br /><br /> Passphrase<br /><br /> Porta di Amministrazione centrale SharePoint|Predefinito, se necessario|Per le impostazioni, vengono usati come predefiniti i valori immessi nella pagina principale.|  
|**Configurare l'istanza del servizio locale**|Password dell'account del servizio Analysis Services|Input dell'utente|È necessario digitare la password dell'account del servizio Analysis Services nel **registrare SQL Server Analysis Services (PowerPivot) sul Server locale** pagina.<br /><br /> L'account del servizio è stato specificato durante l'installazione. È necessario digitare la password come input per la registrazione dell'istanza del servizio locale con SharePoint.|  
|**Creare applicazione del servizio PowerPivot**|Nome dell'applicazione del servizio PowerPivot|Impostazione predefinita|Il nome predefinito è Applicazione di servizio PowerPivot predefinita. È possibile usare un valore diverso nello strumento.|  
||Server di database dell'applicazione del servizio PowerPivot|Impostazione predefinita|Server di database che ospita il database dell'applicazione di servizio PowerPivot. Il nome del server predefinito corrisponde al server di database usato per la farm. È possibile usare un valore diverso nello strumento.|  
||Nome del database dell'applicazione del servizio PowerPivot|Impostazione predefinita|Il nome del database predefinito è basato sul nome dell'applicazione del servizio, seguito da un GUID per assicurarne l'univocità. È possibile usare un valore diverso nello strumento.|  
||Aggiorna le cartelle di lavoro per abilitare l'aggiornamento dei dati|Input dell'utente|L'aggiornamento dei dati ha esito negativo e non è supportato per le cartelle di lavoro di SQL Server 2008 R2 PowerPivot. L'opzione **cartelle di lavoro di aggiornamento per abilitare data refresh** Aggiorna le cartelle di lavoro alla versione di SQL Server 2012 PowerPivot.|  
|**Creare applicazione Web predefinita**|Nome applicazione Web|Predefinito, se necessario|Se non esistono applicazioni Web, ne viene creata una. L'applicazione web verrà configurata per l'autenticazione in modalità classica e per l'ascolto **la porta 80**. Le dimensioni di caricamento file massime vengono impostate su 2047 MB, il massimo consentito in SharePoint. Tali dimensioni di caricamento sono necessarie per i file PowerPivot di grandi dimensioni.|  
||URL|Predefinito, se necessario|Viene creato un URL in base al nome del server, usando le stesse convenzioni di denominazione per i nomi file di SharePoint.|  
||Pool di applicazioni Web|Predefinito, se necessario|Viene creato un pool di applicazioni predefinito in IIS.|  
||Account e password pool di applicazioni Web|Predefinito, se necessario|L'account del pool di applicazioni è basato sull'account predefinito, anche se è possibile eseguirne l'override nello strumento.|  
||Server di database dell'applicazione Web|Predefinito, se necessario|L'istanza del database predefinito viene pre-selezionata per archiviare il database dell'applicazione, tuttavia è possibile specificare un'istanza di SQL Server diversa nello strumento.|  
||Nome del database dell'applicazione Web|Predefinito, se necessario|Il nome del database è basato sulle convenzioni di denominazione per i nomi file di SharePoint, tuttavia è possibile scegliere un nome diverso.|  
|**Distribuire la soluzione applicazione Web**|URL|Predefinito, se necessario|L'URL predefinito è quello dell'applicazione Web predefinita.|  
||Dimensioni massime file (in MB)|Predefinito, se necessario|L'impostazione predefinita è 2047. Le raccolte documenti di SharePoint hanno anche una dimensione massima e l'impostazione di PowerPivot non deve superare quella della raccolta documenti. Per altre informazioni, vedere [configurare dimensioni di caricamento File massime &#40;PowerPivot per SharePoint&#41;](power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).|  
|**Creare raccolta siti**|Amministratore del sito|Predefinito, se necessario|Viene usato l'account predefinito. È possibile eseguire l'override di questo account nella pagina **Creare raccolta siti** .|  
||Posta elettronica contatto|Predefinito, se necessario|Se Microsoft Outlook è configurato nel server, viene usato l'indirizzo di posta elettronica dell'utente corrente. In caso contrario, viene usato un segnaposto.|  
||URL sito|Predefinito, se necessario|Viene creato l'URL del sito usando le stesse convenzioni di denominazione per gli URL di SharePoint.|  
||Titolo sito|Predefinito, se necessario|Come titolo predefinito viene aggiunto **Sito PowerPivot** .|  
|**Attivare la funzionalità di PowerPivot in una raccolta siti**|URL sito||URL della raccolta siti per cui si stanno attivando le funzionalità di PowerPivot.|  
||Abilitare la funzionalità avanzata per questo sito||Abilitare la funzionalità "premiumsite" per siti SharePoint.|  
|**Creare applicazione del servizio di archiviazione sicura**|Nome applicazione di servizio||Digitare il nome per l'applicazione del servizio di archiviazione sicura.|  
||Server di database||Digitare il nome del server di database da usare per l'applicazione del servizio di archiviazione sicura.|  
|**Creare proxy applicazione del servizio di archiviazione sicura**|Nome applicazione di servizio||Digitare il nome per l'applicazione del servizio di archiviazione sicura.|  
||Proxy applicazione del servizio||Digitare il nome per il proxy dell'applicazione del servizio di archiviazione sicura.  Il nome verrà visualizzato nel gruppo di connessione predefinito che associa le applicazioni alle applicazioni Web di contenuto SharePoint.|  
|**Aggiornare la chiave master del servizio di archiviazione sicura**|Proxy applicazione del servizio||Digitare il nome per il proxy dell'applicazione del servizio di archiviazione sicura|  
||Passphrase||Per la crittografia dei dati viene usata la chiave master. Per impostazione predefinita, la passphrase usata per generare la chiave è identica a quella usata per il provisioning di nuovi server nella farm. È possibile sostituire la passphrase predefinita con una passphrase univoca.|  
|**Creare Account automatico per Datarefresh**|ID applicazione di destinazione||L'ID applicazione può essere un testo descrittivo.|  
||Nome descrittivo per l'applicazione di destinazione|||  
||Nome utente e password account automatico||Digitare le credenziali di un account utente di Windows usato dall'applicazione di destinazione e usato per eseguire l'aggiornamento automatico dei dati.|  
||URL sito||Digitare l'URL sito della raccolta siti associata all'applicazione di destinazione. Per l'associazione con raccolte siti aggiuntive, usare Amministrazione centrale SharePoint.|  
|**Crea applicazione di servizio per Excel Services**|Nome applicazione di servizio||Digitare un nome per l'applicazione di servizio. Verrà creato un database dell'applicazione di servizio con lo stesso nome nel server di database della farm SharePoint.|  
|**Aggiungere MSOLAP.5 come Provider attendibile**|Nome applicazione di servizio||Excel Services in SharePoint 2010 usano il provider OLE DB di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per connettersi ai dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Con questo passaggio viene aggiunta la versione del provider OLE DB installata con PowerPivot per SharePoint come provider di dati attendibile in Excel Services.|  
||Nome server PowerPivot|||  
|||||  
  
 Se tramite lo strumento di configurazione PowerPivot viene creata la farm, i database necessari vengono creati nel server di database usando le stesse convenzioni di denominazione per i nomi file di SharePoint. Non è possibile modificare il nome del database della farm.  
  
 Se viene creata una raccolta siti, il database del contenuto viene creato nel server di database usando le stesse convenzioni di denominazione per i nomi file di SharePoint. Non è possibile modificare il nome del database del contenuto.  
  
##  <a name="bkmk_nextsteps"></a> Passaggi successivi  
 Dopo aver completato l'installazione di un server, è necessario effettuare diverse attività post-installazione:  
  
-   Concedere le autorizzazioni SharePoint a singoli e gruppi. Questa attività è necessaria per consentire l'accesso a siti e contenuti.  
  
-   Modificare le identità del pool di applicazioni del servizio per l'esecuzione in un account diverso. La definizione di identità diverse per servizi e applicazioni è una procedura SharePoint consigliata per le distribuzioni sicure.  
  
-   Creare siti attendibili aggiuntivi in Excel Services in modo da poter variare le autorizzazioni e le impostazioni di configurazione che funzionano meglio per l'accesso ai dati PowerPivot.  
  
-   Installare ADO.NET Data Services 3.5 SP1 per abilitare l'esportazione dei feed di dati dagli elenchi SharePoint.  
  
-   Installare provider di dati di uso comune per abilitare l'aggiornamento dati lato server.  
  
-   Scaricare lo strumento di creazione di PowerPivot sul computer della workstation in uso per creare una cartella di lavoro di PowerPivot e pubblicarla quindi su SharePoint. L'installazione dello strumento e la pubblicazione di una cartella di lavoro di PowerPivot completano il ciclo di installazione verificando l'interoperabilità dei componenti server appena installati.  
  
### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Concedere autorizzazioni di SharePoint agli utenti delle cartelle di lavoro  
 Gli utenti devono disporre delle autorizzazioni di SharePoint per pubblicare o visualizzare cartelle di lavoro. Assicurarsi di concedere **View** le autorizzazioni per gli utenti che devono visualizzare cartelle di lavoro pubblicate e **collaborazione** delle autorizzazioni per gli utenti che pubblicano o gestiscono le cartelle di lavoro. Per concedere le autorizzazioni, è necessario disporre dei privilegi di amministratore della raccolta siti.  
  
1.  Nel sito, fare clic su **Azioni sito**.  
  
2.  Fare clic su **autorizzazioni sito**.  
  
3.  Creare gruppi in base alle esigenze se si desidera un set di utenti con autorizzazioni **Collaborazione** e un altro gruppo per un set di utenti che dispongono solo delle autorizzazioni **Visualizza** .  
  
4.  Immettere gli account gruppo o utente di dominio di Windows con appartenenza ai gruppi. Come in precedenza, non usare indirizzi di posta elettronica o gruppi di distribuzione se l'applicazione è configurata per l'autenticazione classica.  
  
### <a name="install-adonet-data-services-35-sp1"></a>Installare ADO.NET Data Services 3.5 SP1  
 ADO.NET Data Services è necessario per un'esportazione dei feed di dati di elenchi SharePoint. SharePoint 2010 non include questo componente nel programma PrerequisiteInstaller, pertanto è necessario installarlo manualmente.  
  
1.  Passare alla documentazione di requisiti hardware e software per SharePoint 2010, [determinare requisiti Hardware e Software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  Nella sezione relativa ai prerequisiti software di installazione cercare il collegamento per ADO.NET Data Services 3.5 che corrisponde al sistema operativo in uso.  
  
3.  Fare clic sul collegamento ed eseguire il programma di installazione che consente di installare il servizio.  
  
### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Installare provider di dati usati per l'aggiornamento dati e verificare le autorizzazioni utente  
 L'aggiornamento dati lato server consente agli utenti di reimportare dati aggiornati nelle cartelle di lavoro in modalità automatica. Affinché l'aggiornamento dati riesca, il server deve disporre dello stesso provider di dati usato per importare i dati inizialmente. Inoltre, per l'account utente con il quale viene eseguito l'aggiornamento dati vengono spesso richieste autorizzazioni di lettura sulle origini dati esterne. Verificare i requisiti per l'abilitazione e la configurazione dell'aggiornamento dati per assicurarsi un risultato positivo. Per altre informazioni, vedere [aggiornamento dati PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md).  
  
### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>Modificare il pool di applicazioni e le identità di servizio in SharePoint  
 Tramite lo strumento di configurazione PowerPivot viene eseguito il provisioning delle funzionalità della farm, delle applicazioni e dei servizi affinché vengano eseguiti con un singolo account. L'installazione risulterà semplificata, ma la distribuzione non soddisferà i requisiti di sicurezza di una farm di SharePoint. Per creare una distribuzione più affidabile, modificare i pool di applicazioni e le identità di servizio affinché l'esecuzione avvenga in account diversi al termine dell'installazione. Per altre informazioni, vedere [configurare account di servizio PowerPivot](power-pivot-sharepoint/configure-power-pivot-service-accounts.md).  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>Creare siti attendibili aggiuntivi in Excel Services  
 È possibile aggiungere siti attendibili in Excel Services per variare le autorizzazioni e le impostazioni di configurazione nei siti che forniscono cartelle di lavoro di Excel e dati PowerPivot. Per altre informazioni, vedere [Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale](power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
### <a name="add-servers-or-applications"></a>Aggiungere server o applicazioni  
 Nel tempo, se si rendessero necessarie ulteriori funzionalità di elaborazione e archiviazione dati, sarà possibile aggiungere una seconda istanza del server PowerPivot per SharePoint alla farm. Per istruzioni, vedere [elenco di controllo distribuzione: Scalabilità orizzontale aggiungendo server PowerPivot a una farm di SharePoint 2010](../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
## <a name="additional-resources"></a>Risorse aggiuntive  
 ![Impostazioni di SharePoint](media/as-sharepoint2013-settings-gear.gif "impostazioni SharePoint") [Invia commenti e suggerimenti e informazioni di contatto tramite Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di configurazione PowerPivot](power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
