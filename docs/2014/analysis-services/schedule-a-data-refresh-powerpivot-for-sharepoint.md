---
title: Pianificare un aggiornamento di dati (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 8571208f-6aae-4058-83c6-9f916f5e2f9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 429b35f6865deb5c0c3dd79e21cfe16cac7fae91
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070004"
---
# <a name="schedule-a-data-refresh-powerpivot-for-sharepoint"></a>Pianificare un aggiornamento dati (PowerPivot per SharePoint)
  È possibile pianificare aggiornamenti automatici dei dati PowerPivot in una cartella di lavoro di Excel pubblicata in un sito di SharePoint.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 **Contenuto dell'argomento:**  
  
 [Prerequisiti](#prereq)  
  
 [Panoramica dell'aggiornamento dati](#intro)  
  
 [Abilitare e pianificare l'aggiornamento dati](#drenablesched)  
  
 [Verificare l'aggiornamento dati](#drverify)  
  
> [!NOTE]  
>  L'aggiornamento dati PowerPivot viene eseguito dalle istanze del server Analysis Services nella farm di SharePoint. Non è correlato alla funzionalità di aggiornamento dati fornita in Excel Services. La funzionalità Pianificazione dell'aggiornamento dati non aggiornerà i dati non PowerPivot.  
  
##  <a name="prereq"></a> Prerequisiti  
 Per creare una pianificazione dell'aggiornamento dati è necessario disporre almeno del livello di autorizzazione di collaborazione relativamente alla cartella di lavoro.  
  
 Devono essere disponibili le origini dati esterne a cui si accede durante l'aggiornamento dati e le credenziali specificate nella pianificazione devono consentire di accedere a tali origini dati. L'aggiornamento dati pianificato richiede l'accesso a un percorso origine dati tramite una connessione di rete (ad esempio da una condivisione file di rete piuttosto che da una cartella locale nella workstation).  
  
 L'origine dati non può essere un documento di Office o un database di Access. Office non supporta l'utilizzo dei componenti per la connettività dei dati di Office in un ambiente server. Se nella cartella di lavoro sono contenuti dati da queste origini, assicurarsi di rimuovere tali origini dall'elenco dell'origine dati nella pianificazione dell'aggiornamento dati.  
  
 La cartella di lavoro deve essere la versione [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] . Se si usano cartelle di lavoro create nella versione precedente di PowerPivot per Excel, la pianificazione dell'aggiornamento dati non funzionerà a meno che non si aggiorni il database alla versione più recente.  
  
 La cartella di lavoro deve essere archiviata al termine dell'operazione di aggiornamento. Un blocco nella cartella di lavoro viene posizionato sul file alla fine dell'aggiornamento dei dati, quando il file viene salvato, anziché quando l'aggiornamento viene avviato.  
  
> [!NOTE]  
>  Il server non consente di bloccare la cartella di lavoro mentre l'aggiornamento dei dati è in corso. Tuttavia, consente di bloccare il file alla fine dell'aggiornamento allo scopo di archiviare il file aggiornato. Se a questo punto, il file viene estratto da un altro utente, i dati aggiornati saranno eliminati. Analogamente, se il file viene archiviato ma è molto diverso dalla copia recuperata dal server all'inizio dell'aggiornamento dati, i dati aggiornati saranno rimossi.  
  
##  <a name="intro"></a> Panoramica dell'aggiornamento dati  
 I dati PowerPivot in una cartella di lavoro di Excel possono provenire da più origini dati esterne, inclusi database esterni o file di dati ai quali si accede da server remoti o da condivisioni file di rete. Per le cartelle di lavoro di PowerPivot in cui sono contenuti i dati importati da origini dati connesse o esterne, è possibile configurare l'aggiornamento dei dati per pianificare un'importazione automatica di dati aggiornati da tali origini iniziali.  
  
 L'accesso a un'origine dati esterna viene eseguito tramite una stringa di connessione incorporata, un URL o un percorso UNC specificati quando i dati originali sono stati importati nella cartella di lavoro tramite l'applicazione client di PowerPivot. Le informazioni di connessione originali archiviate nella cartella di lavoro di PowerPivot vengono riutilizzate per le successive operazioni di aggiornamento dati. Sebbene sia possibile sovrascrivere le credenziali usate per connettersi alle origini dati, non è possibile sovrascrivere le stringhe di connessione per ragioni di aggiornamento dati; vengono usate solo le informazioni di connessione esistenti.  
  
 È disponibile una sola pagina della pianificazione di aggiornamento dei dati per ogni cartella di lavoro e tutte le informazioni sulla pianificazione vengono specificate in quella pagina. In genere, l'utente che ha creato la cartella di lavoro definisce la pianificazione.  
  
 In qualità di proprietario della pianificazione è possibile effettuare le attività seguenti:  
  
-   Definire la pianificazione predefinita. È la pianificazione usata se è nessuna programmazione è definita a livello di origine dati.  
  
-   Specificare le credenziali usate per eseguire l'aggiornamento dei dati  
  
-   Scegliere le origini dati da includere nell'operazione di aggiornamento.  
  
-   Facoltativamente, specificare pianificazioni e credenziali singole inline per ogni origine dati su cui vengono eseguite le query durante l'aggiornamento dei dati. Ogni origine dati può essere aggiornata indipendentemente. Se si creano pianificazioni personalizzate per ogni origine dati, la pianificazione predefinita viene ignorata.  
  
 La creazione di pianificazioni granulari per singole origini dati consente di associare la pianificazione dell'aggiornamento alle fluttuazioni nelle origini dati esterne. Ad esempio, se in un'origine dati esterna sono contenuti dati transazionali generati durante il giorno, è possibile creare una singola pianificazione dell'aggiornamento dei dati per tale origine dati per ottenere le informazioni aggiornate di notte.  
  
##  <a name="drenablesched"></a> Abilitare e pianificare l'aggiornamento dati  
 Usare le istruzioni seguenti per pianificare l'aggiornamento dei dati PowerPivot in una cartella di lavoro di Excel pubblicata in una raccolta di SharePoint.  
  
1.  Nella raccolta in cui è contenuta la cartella di lavoro, selezionare la cartella di lavoro, quindi fare clic sulla freccia GIÙ per visualizzare un elenco di comandi.  
  
2.  Fare clic su **Gestire l'aggiornamento dati PowerPivot**. Se è già stata definita una pianificazione dell'aggiornamento dei dati, verrà invece visualizzata la pagina della cronologia di visualizzazione dell'aggiornamento dei dati. È possibile scegliere l'opzione di **configurazione dell'aggiornamento dei dati** per aprire la pagina di definizione della pianificazione.  
  
3.  Nella pagina di definizione della pianificazione, selezionare la casella di controllo **Abilita** .  
  
4.  In Dettagli pianificazione specificare il tipo di pianificazione e specificare i relativi dettagli. Con questo passaggio viene creata la pianificazione predefinita.  
  
    > [!IMPORTANT]  
    >  Assicurarsi di selezionare la casella di controllo **Aggiorna anche appena possibile** . In questo modo è possibile verificare che l'aggiornamento dati sia operativo per questa cartella di lavoro. Dopo avere salvato la pianificazione, l'avvio dell'aggiornamento dati potrebbe richiedere fino a un minuto.  
  
5.  In Prima ora di inizio scegliere uno degli elementi seguenti:  
  
    1.  Tramite l'opzione**Dopo l'orario di ufficio** viene specificato un periodo di elaborazione dopo le ore di lavoro stabilite quando è più probabile che i server di database dispongano dei dati correnti generati durante tutto il giorno lavorativo.  
  
    2.  **Prima ora di inizio specifica** rappresenta l'ora e i minuti esatti della prima ora del giorno in cui la richiesta di aggiornamento dei dati viene aggiunta a una coda dei processi. I minuti possono essere specificati in intervalli di 15 minuti. L'impostazione si applica al giorno corrente e alle date future. Ad esempio, se si specifica un valore pari alle 6.30 e l'ora corrente è 16.30, la richiesta di aggiornamento verrà aggiunta alla coda del giorno corrente in quanto le 16.30 sono successive alle 6.30.  
  
     Tramite la prima ora di inizio viene definito il momento in cui una richiesta viene aggiunta alla coda dei processi. L'elaborazione effettiva si verifica quando il server dispone di risorse adatte per iniziare l'elaborazione dati. Il tempo dell'elaborazione effettiva sarà registrato nella cronologia dell'aggiornamento dati dopo il completamento dell'elaborazione.  
  
6.  Selezionare la casella di controllo **Aggiorna anche appena possibile** per eseguire l'aggiornamento dati appena questa operazione potrà essere elaborata dal server. Un risultato positivo di un processo di aggiornamento dati dimostra che le origini dati sono disponibili e che le autorizzazioni e la configurazione del server sono state impostate correttamente.  
  
7.  In Notifiche tramite posta elettronica immettere l'indirizzo di posta elettronica della persona che deve essere notificata in caso di errore di elaborazione.  
  
8.  In Credenziali specificare un account usato per eseguire il processo di aggiornamento dati. L'account deve disporre delle autorizzazioni di collaborazione sulla cartella di lavoro, affinché tale cartella possa essere aperta per l'aggiornamento dei relativi dati, e deve essere un account utente di dominio Windows. In molti casi, questo account deve disporre anche delle autorizzazioni di lettura sulle origini dati esterne usate durante l'aggiornamento dati. In particolare, se sono stati importati originalmente i dati usando l'opzione Usa autenticazione di Windows, la stringa di connessione è compilata per usare le credenziali di Windows dell'utente corrente. Se l'utente corrente è l'account di aggiornamento dati, tale account deve disporre delle autorizzazioni di lettura sull'origine dati esterna affinché l'aggiornamento dati venga completato correttamente. Selezionare una delle opzioni seguenti:  
  
    1.  Scegliere **Utilizza l'account di aggiornamento dati configurato dall'amministratore** per elaborare l'operazione di aggiornamento dati usando l'account di aggiornamento dati automatico PowerPivot.  
  
    2.  Scegliere **Effettua la connessione con le seguenti credenziali utente di Windows** se si desidera immettere un nome utente e una password. Immettere le informazioni dell'account nel formato dominio\utente.  
  
    3.  Scegliere **Effettua la connessione usando le credenziali salvate nel servizio di archiviazione sicura** se si conosce l'ID di un'applicazione di destinazione in cui sono contenute le credenziali precedentemente archiviate che si desidera usare.  
  
     Per altre informazioni su queste opzioni, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41; ](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) e [configurare l'Account di aggiornamento dati PowerPivot automatico &#40;PowerPivot per SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
9. In Origini dati selezionare la casella di controllo **Tutte le origini dati** se si desidera che tramite l'aggiornamento dati venga di nuovo eseguita una query su tutte le origini dati iniziali.  
  
     Se si seleziona questa opzione, qualsiasi origine dati esterna che fornisce dati PowerPivot viene inclusa automaticamente nell'aggiornamento, anche se l'elenco di origini dati viene modificato nel tempo quando si aggiungono o rimuovono le origini dati che forniscono dati alla cartella di lavoro.  
  
     Deselezionare la casella di controllo **Tutte le origini dati** se si desidera selezionare manualmente le origini dati da includere. Se successivamente si modifica la cartella di lavoro aggiungendo una nuova origine dati, assicurarsi di aggiornare l'elenco delle origini dati nella pianificazione. In caso contrario, le origini dati più recenti non saranno incluse nell'operazione di aggiornamento.  
  
     L'elenco di origini dati da cui è possibile scegliere viene recuperato dalla cartella di lavoro di PowerPivot quando viene aperta la pagina Gestisci aggiornamento dati PowerPivot per la cartella di lavoro.  
  
     Assicurarsi di selezionare solo le origini dati che soddisfano i criteri seguenti:  
  
    -   L'origine dati deve essere disponibile quando si verifica l'aggiornamento dei dati e nel percorso dichiarato. Se l'origine dati iniziale si trova in un'unità disco locale della persona che ha creato la cartella di lavoro, è necessario escludere tale origine dati dall'operazione di aggiornamento dei dati o individuare un modo per pubblicare tale origine dati in un percorso accessibile tramite una connessione di rete. Se si sposta un'origine dati in un percorso di rete, assicurarsi di aprire la cartella di lavoro in [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] e di aggiornare le informazioni di connessione all'origine dati. Questa operazione è necessaria per riattivare le informazioni di connessione archiviate nella cartella di lavoro di PowerPivot.  
  
    -   L'accesso all'origine dati deve essere eseguito usando le informazioni sulle credenziali incorporate nella cartella di lavoro di PowerPivot o specificate nella pianificazione. Le informazioni sulle credenziali incorporate vengono archiviate nella cartella di lavoro di PowerPivot quando si importano dati usando PowerPivot per Excel. Tali informazioni sono spesso SSPI=IntegratedSecurity o SSPI=TrustedConnection, pertanto la connessione all'origine dati viene eseguita usando le credenziali dell'utente corrente. Se si desidera eseguire l'override delle informazioni sulle credenziali nella pianificazione dell'aggiornamento dati, è possibile specificare le credenziali archiviate predefinite. Per altre informazioni, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
    -   L'aggiornamento dei dati deve avere un esito positivo per tutte le origini dati specificate. In caso contrario, i dati aggiornati vengono rimossi e viene mantenuta l'ultima versione salvata della cartella di lavoro. Escludere tutte le origini dati di cui non si è sicuri.  
  
    -   L'aggiornamento dei dati non deve invalidare altri dati della cartella di lavoro. Quando si aggiorna un subset di dati, è importante capire se la cartella di lavoro è ancora valida una volta che i dati più recenti vengono aggregati con i dati statici che non derivano dallo stesso periodo di tempo. In qualità di autore della cartella di lavoro, l'utente deve conoscere le dipendenze dei propri dati e assicurarsi che l'aggiornamento dei dati sia adatto per la cartella di lavoro.  
  
10. Facoltativamente, è possibile definire singole pianificazioni per le origini dati specifiche. Questa operazione è utile se si dispone di origini dati iniziali che vengono anch'esse aggiornate in una pianificazione. Ad esempio, se in un'origine dati PowerPivot vengono usati dati di un data mart aggiornato ogni lunedì alle 02.00, è possibile definire una pianificazione inline affinché il data mart consenta di recuperare i dati aggiornati ogni lunedì alle 04.00.  
  
11. Scegliere **OK** per salvare la pianificazione.  
  
##  <a name="drverify"></a> Verificare l'aggiornamento dati  
 Il modo migliore per verificare l'aggiornamento dati consiste nell'eseguire subito questa operazione e di esaminare la pagina della cronologia per controllare se l'aggiornamento è stato completato correttamente. Selezionare la casella di controllo **Aggiorna anche appena possibile** per verificare che l'aggiornamento dati è operativo.  
  
 È possibile visualizzare il record corrente e passato delle operazioni di aggiornamento dati nella pagina Cronologia aggiornamento dati per la cartella di lavoro. Questa pagina viene visualizzata solo se l'aggiornamento dei dati è stato pianificato per una cartella di lavoro. Se non esiste nessuna pianificazione dell'aggiornamento dei dati, viene visualizzata la pagina di definizione della pianificazione.  
  
 È necessario disporre di autorizzazioni di collaborazione o superiori per visualizzare la cronologia dell'aggiornamento dei dati.  
  
1.  In un sito di SharePoint aprire la raccolta in cui è inclusa una cartella di lavoro di PowerPivot.  
  
     Non viene visualizzato alcun indicatore che consenta di identificare le cartelle di lavoro di una raccolta di SharePoint contenenti dati PowerPivot. È necessario sapere in anticipo in quali cartelle di lavoro sono inclusi dati PowerPivot aggiornabili.  
  
2.  Selezionare il documento, quindi fare clic sulla freccia GIÙ visualizzata a destra.  
  
3.  Selezionare **Gestisci aggiornamento dati PowerPivot**.  
  
 Viene visualizzata la pagina della cronologia in cui viene mostrato un record completo per ogni attività di aggiornamento per i dati PowerPivot nella cartella di lavoro di Excel corrente, incluso lo stato dell'operazione di aggiornamento dei dati più recente.  
  
 In alcuni casi, è possibile visualizzare tempi di elaborazione effettivi diversi da quelli specificati. Questa situazione si verifica se il carico di elaborazione nel server è pesante. In tal caso, prima di avviare un aggiornamento dei dati, l'istanza del servizio [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] rimarrà in ascolto finché non sono disponibili risorse di sistema sufficienti.  
  
 La cartella di lavoro deve essere archiviata al termine dell'operazione di aggiornamento durante la quale sarà anche salvata con i dati aggiornati. Se il file viene estratto, l'aggiornamento dei dati viene ignorato fino alla successiva pianificazione.  
  
 Se viene visualizzato un messaggio di stato imprevisto (ad esempio l'esito negativo o l'annullamento di un'operazione di aggiornamento), è possibile esaminare il problema controllando le autorizzazioni e la disponibilità dei server.  
  
 Controllare la pagina sulla risoluzione dei problemi relativi all'aggiornamento dati PowerPivot in TechNet WIKI per un supporto sulla risoluzione di problemi di questo tipo. Per altre informazioni, vedere l'articolo sulla [risoluzione dei problemi relativi all'aggiornamento dati PowerPivot](https://go.microsoft.com/fwlink/?LinkId=251594).  
  
> [!NOTE]  
>  Gli amministratori di SharePoint possono assistere nella risoluzione dei problemi relativi all'aggiornamento dei dati visualizzando i report consolidati sull'aggiornamento dei dati nel Dashboard di gestione PowerPivot in Amministrazione centrale. Per ulteriori informazioni, vedere [PowerPivot Management Dashboard and Usage Data](power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dati PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Visualizzare la cronologia aggiornamento dati &#40;PowerPivot per SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)   
 [Configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
