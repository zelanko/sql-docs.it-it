---
title: Configurare o ripristinare PowerPivot per SharePoint 2013 (strumento di configurazione PowerPivot) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 616877e3-464a-4c97-bc74-1fa6f4faa756
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84418ca3f32700831eaac6b344f50f9cc862625a
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175700"
---
# <a name="configure-or-repair-powerpivot-for-sharepoint-2013-powerpivot-configuration-tool"></a>Configurare o ripristinare PowerPivot per SharePoint 2013 (strumento di configurazione PowerPivot)
  Per configurare o ripristinare un'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013, usare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint. Tramite lo strumento di configurazione viene innanzitutto analizzato il sistema, dopodiché viene restituito un elenco di azioni necessarie per completare o ripristinare l'installazione. L'Installazione guidata [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] consente di installare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2010 e lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013. In questo argomento viene descritto lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013. Per ulteriori informazioni su SharePoint 2010, vedere [configurare o ripristinare PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md).

 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013

 **Contenuto dell'argomento:**

 [Prima di iniziare](#bkmk_before)

 [Per utilizzare lo strumento di configurazione PowerPivot per SharePoint 2013](#bkmk_using)

 [Passaggi di configurazione](#bkmk_steps)

 [Valori di input usati per configurare il server](#bkmk_input)

 [Passaggi successivi](#bkmk_nextsteps)

##  <a name="bkmk_before"></a>Prima di iniziare
 Lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013 esegue l'analisi di file di programma, impostazioni del Registro di sistema e porte disponibili. Per usare al meglio gli strumenti, vedere gli argomenti seguenti.

-   Requisiti generali per eseguire lo strumento di configurazione, [PowerPivot Configuration Tools](power-pivot-configuration-tools.md).

-   
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013 si preferisce un'applicazione Web configurata per l'autenticazione basata sulle attestazioni. Se viene creata automaticamente tramite lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013, l'applicazione è configurata per l'utilizzo dell'autenticazione di Windows basata sulle attestazioni. Per ulteriori informazioni sui requisiti di autenticazione, vedere [PowerPivot Authentication and Authorization](power-pivot-authentication-and-authorization.md).

-   Per la creazione di un'applicazione Web tramite lo strumento di configurazione[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013 deve essere disponibile la porta 80.

##  <a name="bkmk_using"></a>Per utilizzare lo strumento di configurazione PowerPivot per SharePoint 2013
 Nella prima pagina dello strumento viene fornito un riepilogo dei valori di input usati per configurare la farm di SharePoint. Oltre ai valori di input che è necessario specificare, per configurare il sistema sono necessari dei valori predefiniti. Vengono usati nomi predefiniti per applicazioni del servizio, database di applicazioni del servizio e proprietà di applicazioni del servizio.

> [!TIP]
>  Se tramite lo strumento di configurazione viene eseguita l'analisi del computer e viene restituito un elenco di attività vuoto nel riquadro sinistro, non è necessaria la configurazione per alcuna funzionalità o impostazione. Per modificare la configurazione di SharePoint o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , utilizzare Windows PowerShell o le pagine di gestione in Amministrazione centrale SharePoint. Per ulteriori informazioni, vedere [amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md).

 I valori per gli account del servizio sono usati per più servizi. Ad esempio, l'account predefinito viene utilizzato dallo strumento di configurazione nella prima pagina per impostare tutte le identità del pool di applicazioni. È possibile cambiare questi account in un secondo momento modificando le proprietà dell'applicazione di servizio in Amministrazione centrale.

 Lo strumento dispone di un'interfaccia a schede comprendente input di parametri, script di Windows PowerShell e messaggi di stato.

 Inoltre, per la configurazione del server, viene utilizzato Windows PowerShell. Per rivedere lo script di Windows PowerShell utilizzato dallo strumento per configurare il server, fare clic sulla scheda **Script** .

 ![Strumento di configurazione di PowerPivot per SharePoint 2013](../media/ssas-powerpivot-configtool-4-sharepoint2013-mainpage-configure.gif "Strumento di configurazione di PowerPivot per SharePoint 2013")

||Descrizione|
|-|-----------------|
|**1**|Finestra Elenco attività.|
|**2**|Singole azioni.|
|**3**|Script di Windows PowerShell creati dallo strumento di configurazione.|
|**4**|Messaggi del log creati all'avvio della convalida o durante l'esecuzione delle azioni.|
|**5**|Descrizione della pagina.|
|**6**|Parametri di input|
|**7**|Il pulsante **Esegui** viene abilitato dopo avere convalidato le azioni.|

##  <a name="bkmk_steps"></a>Procedura di configurazione
 Il collegamento allo strumento di configurazione è visibile solo quando PowerPivot per SharePoint 2013 è installato nel server locale.

1.  Nel menu **Start** scegliere **Tutti i programmi**, fare clic su [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**, quindi selezionare **Configurazione di PowerPivot per SharePoint 2013**.

2.  Fare clic su **Configura o ripristina PowerPivot per SharePoint**.

3.  Espandere completamente la finestra. Nella parte inferiore della finestra dovrebbe essere disponibile una barra contenente i comandi **Convalida**, **Esegui**ed **Esci** .

4.  **Account predefinito:** Nella scheda parametri digitare un account utente di dominio per il **nome utente dell'account predefinito**. L'account è utilizzato per eseguire il provisioning di servizi essenziali, incluso il pool di applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Non specificare un account predefinito quale Servizio di rete o Sistema locale. Le configurazioni tramite cui vengono specificati account predefiniti vengono bloccate dallo strumento.

     **Passphrase:** Digitare una passphrase. Se la farm di SharePoint è nuova, la passphrase viene utilizzata ogni volta che si aggiungono nuovi server o nuove applicazioni alla farm di SharePoint. Se la farm esiste, immettere la passphrase che consente di aggiungere un'applicazione server alla farm.

5.  **Porta:** Facoltativamente, digitare un numero di porta per la connessione all'applicazione Web Amministrazione centrale oppure utilizzare il numero generato casualmente specificato. Viene verificato che il numero sia disponibile prima di fornirlo come opzione.

6.  Nella pagina principale digitare il nome di un server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] eseguito in modalità SharePoint.

7.  Facoltativamente, rivedere i valori di input rimanenti usati per completare ogni azione. Per altre informazioni su ognuno, vedere [Valori di input usati per configurare il server](#bkmk_input) in questo argomento.

8.  Facoltativamente, rimuovere eventuali azioni che non si desidera elaborare. Ad esempio, se si desidera configurare il servizio di archiviazione sicura in un secondo momento, fare clic su **Configurare il servizio di archiviazione sicura**, quindi deselezionare la casella di controllo **Includere l'azione nell'elenco attività**.

9. Fare clic su **Convalida** per verificare se sono disponibili informazioni sufficienti per lo strumento al fine di elaborare le azioni nell'elenco.

10. Fare clic su **Esegui** per elaborare tutte le azioni nell'elenco attività. Il pulsante **Esegui** diventa disponibile dopo la convalida delle azioni. Se **Esegui** non è abilitato, fare clic su **Convalida** .

     Se viene visualizzato un messaggio di errore simile al seguente, verificare che l'istanza di database di SQL Server sia avviata.

    ```
    Cannot connect to the database server instance
    ```

11. [Verificare un'installazione di PowerPivot per SharePoint](../instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).

##  <a name="bkmk_input"></a>Valori di input usati per configurare il server
 Lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è basato sull'utilizzo di una combinazione di valori di input da digitare e di valori predefiniti rilevati o utilizzati automaticamente.

 L'elenco delle azioni visualizzate dallo strumento di configurazione dipende dalla configurazione corrente delle farm di SharePoint. Ad esempio, se la farm di SharePoint è già configurata, non sono disponibili le azioni per la configurazione della farm o per la creazione di un'applicazione Web. È possibile eseguire lo strumento in qualsiasi momento per configurare, ripristinare o rilevare errori di configurazione. Se servizi necessari quali Excel Services o il servizio di archiviazione sicura non sono in esecuzione nella farm, vengono rilevati i servizi mancanti e vengono proposte le opzioni per abilitarli. Se non è necessaria alcuna azione, l'elenco attività è vuoto.

 Nella tabella seguente vengono descritti i valori usati per configurare il server.

|Pagina|Valore di input|Source (Sorgente)|Descrizione|
|----------|-----------------|------------|-----------------|
|**Configurare o ripristinare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint**|Account predefinito|Utente corrente|L'account predefinito è un account utente di Windows di dominio utilizzato per effettuare il provisioning di servizi condivisi nella farm. Viene utilizzato per il provisioning degli elementi seguenti:<br />[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]applicazione di servizio<br />Servizio di archiviazione sicura<br />Excel Services<br />Identità del pool di applicazioni Web<br />Amministratore della raccolta siti<br />L'Installazione guidata [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Per impostazione predefinita, viene utilizzato l'account di dominio dell'utente corrente. È consigliabile sostituire il valore predefinito, a meno che non si configuri un server per fini di valutazione e non di produzione. È possibile modificare in seguito le identità del servizio tramite Amministrazione centrale. Facoltativamente, nello strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] specificare gli account dedicati per gli elementi seguenti:<br /><br /> Applicazione Web, tramite la pagina **Crea applicazione Web predefinita** (supponendo che lo strumento stia creando un'applicazione Web per la farm).<br />[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]account di aggiornamento dati automatico, usando la pagina **Crea account automatico per l'aggiornamento dati** in questo strumento.|
||Server di database|Istanza denominata di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] locale, se disponibile|Se un'istanza del motore di database è installata come istanza denominata di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , il campo del server di database viene popolato dallo strumento con il nome di questa istanza. Se il motore di database non è installato, questo campo è vuoto.<br /><br /> Il **server di database** è un parametro obbligatorio. Può trattarsi di qualsiasi versione o edizione di SQL Server supportata per le farm SharePoint.|
||Passphrase|Input dell'utente|Se si crea una nuova farm, come relativa passphrase viene utilizzata quella immessa. Se si aggiunge [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint a una farm esistente, digitare la passphrase esistente della farm.|
||Porta di Amministrazione centrale SharePoint|Predefinito, se necessario|Se la farm non è configurata, vengono fornite opzioni per creare la farm e un endpoint HTTP ad Amministrazione centrale. Viene selezionato un numero di porta generato casualmente che non è in uso.|
||
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel Services ([NomeServer]\ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])|Input dell'utente|Il server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è necessario in Excel Services per abilitare le caratteristiche principali di PowerPivot. Il nome del server digitato in questa pagina viene aggiunto anche all'elenco nella pagina **Configura server PowerPivot** .|
|**Configurare la nuova farm**|Server di database<br /><br /> Account farm<br /><br /> Passphrase<br /><br /> Porta di Amministrazione centrale SharePoint|Predefinito, se necessario|Per le impostazioni, vengono usati come predefiniti i valori immessi nella pagina principale.|
|**Creare applicazione del servizio PowerPivot**|Nome applicazione di servizio|Predefinito|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Nome dell'applicazione di servizio il nome predefinito è **applicazione di servizio PowerPivot predefinita**. È possibile usare un valore diverso nello strumento.|
||Server di database|Predefinito|Server di database che ospita il database dell'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Il nome del server predefinito corrisponde al server di database usato per la farm. Questo nome può essere sostituito con un valore diverso.|
||Nome database|Predefinito|Nome del database da creare per il database dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Il nome del database predefinito è basato sul nome dell'applicazione del servizio, seguito da un GUID per assicurarne l'univocità. È possibile usare un valore diverso nello strumento.|
|**Crea applicazione Web predefinita**|Nome applicazione Web|Predefinito, se necessario|Se non esistono applicazioni Web, ne viene creata una. L'applicazione Web è configurata per l'autenticazione in modalità classica ed è in ascolto sulla porta 80. Le dimensioni di caricamento file massime vengono impostate su 2047, il massimo consentito in SharePoint. Tali dimensioni di caricamento sono necessarie per i file [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] di grandi dimensioni che verranno caricati nel server.|
||URL|Predefinito, se necessario|Viene creato un URL in base al nome del server, usando le stesse convenzioni di denominazione per i nomi file di SharePoint.|
||Pool di applicazioni|Predefinito, se necessario|Viene creato un pool di applicazioni predefinito in IIS.|
||Account e password del pool di applicazioni|Predefinito, se necessario|L'account del pool di applicazioni è basato sull'account predefinito, anche se è possibile eseguirne l'override nello strumento.|
||Server di database|Predefinito, se necessario|L'istanza del database predefinito viene preselezionata per archiviare il database di contenuto dell'applicazione, tuttavia è possibile specificare un'istanza di SQL Server diversa nello strumento.|
||Nome database|Predefinito, se necessario|Nome del database dell'applicazione. Il nome del database è basato sulle convenzioni di denominazione per i nomi file di SharePoint, tuttavia è possibile scegliere un nome diverso.|
|**Distribuire la soluzione applicazione Web**|URL|Predefinito, se necessario|L'URL predefinito è quello dell'applicazione Web predefinita.|
||Dimensioni massime file (in MB)|Predefinito, se necessario|L'impostazione predefinita è 2047. Le raccolte documenti di SharePoint hanno anche una dimensione massima e l'impostazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non deve superare quella della raccolta documenti. Per altre informazioni, vedere [configurare le dimensioni massime di caricamento dei File &#40;PowerPivot per SharePoint&#41;](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).|
|**Crea raccolta siti**|Amministratore del sito|Predefinito, se necessario|Viene usato l'account predefinito. È possibile eseguire l'override di questo account nella pagina **Creare raccolta siti** .|
||Posta elettronica contatto|Predefinito, se necessario|Se Microsoft Outlook è configurato nel server, viene usato l'indirizzo di posta elettronica dell'utente corrente. In caso contrario, viene usato un segnaposto.|
||Site URL|Predefinito, se necessario|Viene creato l'URL del sito usando le stesse convenzioni di denominazione per gli URL di SharePoint.|
||Titolo sito|Predefinito, se necessario|Come titolo predefinito viene aggiunto **Sito PowerPivot** .|
|**Attivare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] la funzionalità in una raccolta siti**|Site URL||URL della raccolta siti per cui si stanno attivando le funzionalità di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|
||Abilitare la funzionalità avanzata per questo sito||Abilitare la funzionalità del sito di SharePoint "PremiumSite".|
|**Crea applicazione servizio di archiviazione sicura**|Nome applicazione di servizio|Predefinito, se necessario|Digitare il nome per l'applicazione del servizio di archiviazione sicura.|
||Server di database|Input dell'utente|Digitare il nome del server di database da usare per l'applicazione del servizio di archiviazione sicura.|
|**Creare servizio di archiviazione sicura proxy di applicazione**|Nome applicazione di servizio|Predefinito, se necessario|Digitare il nome dell'applicazione del servizio di archiviazione sicura immesso nella pagina precedente.|
||Proxy applicazione del servizio|Predefinito, se necessario|Digitare il nome per il proxy dell'applicazione del servizio di archiviazione sicura. Il nome verrà visualizzato nel gruppo di connessione predefinito che associa le applicazioni alle applicazioni Web di contenuto SharePoint.|
|**Aggiorna chiave master servizio di archiviazione sicura**|Proxy applicazione del servizio|Predefinito, se necessario|Digitare il nome del proxy dell'applicazione del servizio di archiviazione sicura immesso nella pagina precedente.|
||Passphrase|Input dell'utente|Chiave master utilizzata per la crittografia dei dati. Per impostazione predefinita, la passphrase usata per generare la chiave è identica a quella usata per il provisioning di nuovi server nella farm. È possibile sostituire la passphrase predefinita con una passphrase univoca.|
|**Crea account automatico per DataRefresh**|ID applicazione di destinazione|Predefinito, se necessario|Creare un'applicazione di destinazione per archiviare le credenziali utilizzate per l'aggiornamento dati automatico [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> L'ID applicazione può essere un testo descrittivo.|
||Nome descrittivo per l'applicazione di destinazione|Predefinito, se necessario||
||Nome utente e password account automatico|Predefinito, se necessario|Digitare le credenziali di un account utente di Windows utilizzato dall'applicazione di destinazione per eseguire l'aggiornamento dati automatico. Per ulteriori informazioni, vedere [configurare l'aggiornamento dei dati di Excel Services utilizzando l'account del servizio automatico in SharePoint Server 2013](https://technet.microsoft.com/library/hh525344\(office.15\).aspx) (https://technet.microsoft.com/library/hh525344(office.15).aspx).|
||Site URL|Predefinito, se necessario|Digitare l'URL sito della raccolta siti associata all'applicazione di destinazione. Per l'associazione con raccolte siti aggiuntive, usare Amministrazione centrale SharePoint.|
|**Creare un'applicazione di servizio Excel Services**|Nome applicazione di servizio|Predefinito, se necessario|Digitare un nome per l'applicazione di servizio. Nel server di database della farm di SharePoint viene creato un database dell'applicazione di servizio con lo stesso nome.|
|**Configurare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] i server**|Nome applicazione di servizio|Predefinito, se necessario|Nome dell'applicazione di servizio digitato nella pagina precedente.|
||[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Nome del server||Elenco dei server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] registrati.<br /><br /> Il nome del server digitato nella pagina principale viene aggiunto automaticamente in questa pagina.|
|**Registra [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] componente aggiuntivo come Tracker utilizzo di Excel Services**|Nome applicazione di servizio||Nome dell'applicazione di servizio digitato nella pagina precedente.|
|||||

 Se tramite lo strumento di configurazione PowerPivot per SharePoint 2013 viene creata la farm, i database necessari vengono creati nel server di database utilizzando le stesse convenzioni di denominazione per i nomi file di SharePoint. Non è possibile modificare il nome del database della farm.

 Se viene creata una raccolta siti, il database del contenuto viene creato nel server di database usando le stesse convenzioni di denominazione per i nomi file di SharePoint. Non è possibile modificare il nome del database del contenuto.

## <a name="verify-the-configuration"></a>Verificare la configurazione
 Vedere la sezione " [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] verificare la configurazione" di [configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).

##  <a name="bkmk_nextsteps"></a>Passaggi successivi
 Dopo aver completato l'installazione del server, è necessario effettuare diverse attività di post-installazione:

-   Concedere le autorizzazioni SharePoint a singoli e gruppi. Questa attività è necessaria per consentire l'accesso a siti e contenuti.

-   Modificare le identità del pool di applicazioni del servizio per l'esecuzione in un account diverso. La definizione di identità diverse per servizi e applicazioni è una procedura SharePoint consigliata per le distribuzioni sicure.

-   Creare siti attendibili aggiuntivi in Excel Services in modo da variare le autorizzazioni e le impostazioni di configurazione che funzionano meglio per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .

-   Installare provider di dati di uso comune per abilitare l'aggiornamento dati lato server.

### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Concedere autorizzazioni di SharePoint agli utenti delle cartelle di lavoro
 Gli utenti devono disporre delle autorizzazioni di SharePoint per pubblicare o visualizzare cartelle di lavoro. Concedere le autorizzazioni **Visualizzazione** agli utenti che devono visualizzare le cartelle di lavoro pubblicate e le autorizzazioni **Collaborazione** agli utenti che pubblicano o gestiscono le cartelle di lavoro. Per concedere le autorizzazioni, è necessario disporre dei privilegi di amministratore della raccolta siti.

1.  In un sito di SharePoint 2013, fare clic sull'icona delle impostazioni ![impostazioni di SharePoint](../media/as-sharepoint2013-settings-gear.gif "Impostazioni di SharePoint") , quindi fare clic su **Impostazioni sito**.

2.  Nel gruppo **Utenti e autorizzazioni** scegliere **Autorizzazioni sito** .

3.  Creare gruppi in base alle esigenze se si desidera un set di utenti con autorizzazioni **Collaborazione** e un altro gruppo per un set di utenti che dispongono solo delle autorizzazioni **Visualizza** .

4.  Immettere gli account gruppo o utente di dominio di Windows con appartenenza ai gruppi. Come in precedenza, non usare indirizzi di posta elettronica o gruppi di distribuzione se l'applicazione è configurata per l'autenticazione classica.

### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Installare provider di dati usati per l'aggiornamento dati e verificare le autorizzazioni utente
 L'aggiornamento dati lato server consente agli utenti di reimportare dati aggiornati nelle cartelle di lavoro in modalità automatica. Affinché l'aggiornamento dati riesca, il server in cui viene eseguito Analysis Services in modalità SharePoint deve disporre degli stessi provider di dati utilizzati per importare i dati inizialmente. Inoltre, per l'account utente con il quale viene eseguito l'aggiornamento dati vengono spesso richieste autorizzazioni di lettura sulle origini dati esterne. Verificare i requisiti per l'abilitazione e la configurazione dell'aggiornamento dati per assicurarsi un risultato positivo. Per ulteriori informazioni, vedere [aggiornamento dati PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md).

> [!NOTE]
>  Per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013 i provider di dati vengono installati quando si esegue il programma di installazione **spPowerPivot.msi** e lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013. Per ulteriori informazioni, vedere [installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).

### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>Modificare il pool di applicazioni e le identità di servizio in SharePoint
 Tramite lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene eseguito il provisioning delle funzionalità della farm, delle applicazioni e dei servizi affinché vengano eseguiti con un singolo account. L'installazione risulterà semplificata, ma la distribuzione non soddisferà i requisiti di sicurezza di una farm di SharePoint. Per creare una distribuzione più affidabile, modificare i pool di applicazioni e le identità di servizio affinché l'esecuzione avvenga in account diversi al termine dell'installazione. Per ulteriori informazioni, vedere [configurare gli account del servizio PowerPivot](configure-power-pivot-service-accounts.md).

### <a name="create-additional-trusted-sites-in-excel-services"></a>Creare siti attendibili aggiuntivi in Excel Services
 È possibile aggiungere siti attendibili in Excel Services per variare le autorizzazioni e le impostazioni di configurazione nei siti che forniscono cartelle di lavoro di Excel e dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per altre informazioni, vedere [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).

### <a name="build-a-ssgemini-workbook"></a>Compilare una cartella di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]
 Dopo aver installato i componenti server in una farm, è possibile creare la prima cartella di lavoro di Excel 2013 in cui vengono utilizzati dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incorporati e, successivamente, pubblicarla in una raccolta di SharePoint. In alternativa, è possibile caricare o pubblicare una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] di esempio per verificare l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in SharePoint. Per altre informazioni, vedere gli argomenti seguenti:

-   [Novità di PowerPivot in Excel 2013](https://www.microsoft.com/microsoft-365/blog/2012/12/13/introduction-to-powerpivot-in-excel-2013/).

-   [Avviare il componente aggiuntivo PowerPivot in Excel 2013](https://office.microsoft.com/excel-help/start-powerpivot-in-excel-2013-add-in-HA102837097.aspx?CTT=5&origin=HA102837110).

### <a name="add-additional-analysis-services-servers-in-sharepoint-mode"></a>Aggiungere server Analysis Services in modalità SharePoint
 Nel tempo, se si rendessero necessarie ulteriori funzionalità di elaborazione e archiviazione dati, sarà possibile aggiungere ulteriori server Analysis Services in modalità SharePoint alla farm. Per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013, installare nuovi server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint, quindi configurare Excel Services. Per ulteriori informazioni, vedere la sezione "oltre l'installazione a server singolo" dell' [installazione di PowerPivot per SharePoint 2013](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md).

## <a name="additional-resources"></a>Risorse aggiuntive
 ![Le impostazioni di SharePoint](../media/as-sharepoint2013-settings-gear.gif "Impostazioni di SharePoint") [inviano commenti e suggerimenti e informazioni di contatto tramite Microsoft SQL Server Connetti](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).

## <a name="see-also"></a>Vedere anche
 [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;sharepoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md) [PowerPivot strumenti di configurazione](power-pivot-configuration-tools.md) l' [amministrazione e la configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md) [aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)

