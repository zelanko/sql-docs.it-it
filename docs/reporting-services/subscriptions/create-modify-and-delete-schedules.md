---
title: Creare, modificare ed eliminare pianificazioni | Microsoft Docs
ms.date: 06/11/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services]
- modifying schedules
- removing schedules
- shared schedules [Reporting Services], creating
- shared schedules [Reporting Services], modifying
- schedules [Reporting Services], deleting
- deleting schedules
- schedules [Reporting Services], creating
- schedules [Reporting Services], modifying
- shared schedules [Reporting Services], deleting
ms.assetid: 05da5f3d-9222-43a9-893b-aa10f0f690f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29b453914dce3d371ded8f401fd4af0380a115b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "67140218"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  Questo articolo fornisce informazioni sulla creazione, la modifica e l'eliminazione di pianificazioni [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] condivise.  Per gestire le pianificazioni condivise per la modalità nativa, usare la pagina Pianificazioni del portale Web o la cartella Pianificazioni condivise in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per la modalità SharePoint, utilizzare le pagine di gestione per l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

 Per determinare se una pianificazione condivisa è effettivamente usata, usare uno dei metodi seguenti:

-   **Portale Web:** nella scheda **Pianificazione** in **Impostazioni del sito** verificare i valori presenti nei campi Ultima esecuzione, Prossima esecuzione e Stato. Se una pianificazione non viene più eseguita perché è scaduta, nel campo Stato viene visualizzata la data di scadenza. Per altre informazioni, vedere [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).

-   **SQL Server Management Studio:** visualizzando le **report** pagina di una determinata pianificazione condivisa. In questa pagina vengono elencati tutti i report e i set di dati condivisi che utilizzano la pianificazione condivisa. Per altre informazioni, vedere [Reporting Services di SQL Server Management Studio](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md).

-  **Log:** visualizzazione dei file dei log di esecuzione o dei log di traccia del report per verificare se i report sono stati eseguiti negli orari specificati nella pianificazione. Per altre informazioni, vedere [File di log e origini di Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

## <a name="when-you-delete-a-shared-schedule"></a>Eliminazione di una pianificazione condivisa
Le pianificazioni condivise devono essere eliminate manualmente usando la pagina Pianificazioni nel portale Web o la cartella Pianificazioni condivise in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Se si elimina una pianificazione condivisa in uso, tutti i riferimenti a essa verranno sostituiti con pianificazioni in base al report.

Se si elimina una pianificazione condivisa utilizzata da più report e sottoscrizioni, nel server di report vengono create singole pianificazioni per ogni report e sottoscrizione da cui è stata utilizzata in precedenza la pianificazione condivisa. Ogni nuova pianificazione conterrà la data, l'ora e il criterio di occorrenza specificati nella pianificazione condivisa. Si noti che in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è disponibile una funzionalità di gestione centrale delle singole pianificazioni. Se si elimina una pianificazione condivisa, sarà necessario gestire le informazioni sulla pianificazione per ogni elemento singolo.

**Nota:**  in caso di dubbio sull'effettivo uso di una pianificazione condivisa, eliminarla in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] anziché nel portale Web. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] sono disponibili le stesse funzionalità di gestione delle pianificazioni condivise di Gestione report, ma è presente inoltre una pagina Report aggiuntiva contenente il nome di ogni report in cui viene utilizzata la pianificazione.

 Eliminare una pianificazione e farla scadere sono due operazioni diverse. La data di scadenza viene impostata per arrestare una pianificazione, non per eliminarla. Dato che le pianificazioni vengono utilizzate per l'automatizzazione di numerose funzionalità, non vengono mai eliminate automaticamente. Le pianificazioni scadute possono essere utilizzate dagli amministratori del server di report come riscontro per individuare la causa dell'improvviso arresto di un processo automatico. Un amministratore del server di report che non controlla innanzitutto se la pianificazione è scaduta potrebbe eseguire una diagnosi errata del problema oppure perdere inutilmente tempo a cercare di risolvere i problemi di un processo che invece è perfettamente funzionante.

 ## <a name="when-you-delete-a-report-specific-schedule"></a>Eliminazione di una pianificazione in base al report
I report e le pianificazioni specifiche della sottoscrizione vengono eliminati quando si elimina il report o la sottoscrizione o quando si sceglie un approccio diverso per eseguire il report o la sottoscrizione. Se ad esempio si sceglie **Esegui sempre il report con i dati più recenti** , verrà eliminata una pianificazione in base al report creata per eseguire un report come snapshot dell'esecuzione del report stesso.

Una pianificazione in base al report rimane associata al report anche se scaduta. È possibile determinare se una pianificazione è scaduta verificandone la data di fine. Le pianificazioni condivise scadute rimangono comunque nell'elenco della pagina Pianificazioni condivise. Il campo Stato indica se la pianificazione è scaduta. È possibile riattivare la pianificazione posticipando la data di fine oppure rimuovere il riferimento alla pianificazione se non è più necessario.

## <a name="bkmk_native"></a> Creare, eliminare o modificare una pianificazione condivisa (portale Web)
 Le operazioni di creazione e modifica di una pianificazione consistono nell'impostazione delle opzioni di frequenza che determinano quando deve essere eseguita la pianificazione.

 Le pianificazioni possono essere create o modificate in qualsiasi momento. Tuttavia, se l'esecuzione di una pianificazione inizia prima del completamento delle modifiche, verrà utilizzata la versione precedente della pianificazione. La pianificazione modificata ha effetto solo dopo essere stata salvata.

 Se si decide di modificare una pianificazione condivisa, è possibile sospenderla prima di iniziare ad apportarvi le modifiche. Le modifiche avranno effetto quando la pianificazione verrà ripresa.

1. Nel portale Web selezionare **Impostazioni** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) sulla barra degli strumenti.  

   >[!NOTE]  
   >Se **Impostazioni** non è disponibile, non si dispone dell'autorizzazione di accesso alle impostazioni del sito.  

1. Selezionare **Impostazioni sito** nel menu a discesa.
1. Selezionare la scheda **Pianificazioni** .
1. Selezionare **+ nuova pianificazione**. Per modificare una pianificazione esistente, selezionare il nome della pianificazione.
1. Digitare un nome descrittivo per la pianificazione.
1. Selezionare **Ora**, **Giorno**, **Settimana**o **Mese**. Fare clic su **Singola occorrenza** per creare una pianificazione eseguita una sola volta. Dopo aver specificato le impostazioni di base della pianificazione, verranno visualizzate ulteriori opzioni.
1. Selezionare eventualmente la data di inizio della pianificazione. L'impostazione predefinita è il giorno corrente. È possibile posticipare la data di inizio della pianificazione scegliendo una data successiva.
1. Selezionare facoltativamente una data di fine della pianificazione. L'esecuzione della pianificazione verrà arrestata da tale data, ma la pianificazione non verrà eliminata.
1. Selezionare un'ora per la pianificazione per l'esecuzione.
1. Fare clic su **OK**.

### <a name="to-delete-a-shared-schedule-web-portal"></a>Per eliminare una pianificazione condivisa (portale Web)

1. Nel portale Web selezionare **Impostazioni** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) sulla barra degli strumenti.
2. Selezionare **Impostazioni sito** nel menu a discesa.
3. Selezionare la scheda **Pianificazioni** .
4. Selezionare la casella di controllo accanto alla pianificazione condivisa che si vuole eliminare e quindi selezionare **Elimina**.

### <a name="create-delete-or-modify-a-shared-schedule--management-studio"></a>Creare, eliminare o modificare una pianificazione condivisa (Management Studio)
 In una pianificazione condivisa sono contenute le informazioni sulla pianificazione e sull'occorrenza che possono essere utilizzate da qualsiasi numero di sottoscrizioni e report pubblicati in esecuzione in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se il numero di report e sottoscrizioni in esecuzione contemporaneamente è elevato, è possibile creare una pianificazione condivisa per tali processi. Se si desidera modificare successivamente il criterio di occorrenza o la data di fine, è possibile apportare la modifica in un unico punto.

 Le pianificazioni condivise sono più semplici da gestire e consentono una maggiore flessibilità nella gestione di operazioni pianificate. È possibile ad esempio sospendere e quindi riprendere una pianificazione condivisa. Inoltre, se si rileva che sono in esecuzione contemporaneamente troppe operazioni pianificate, sarà possibile creare più pianificazioni condivise per eseguirle in orari diversi, quindi modificare le informazioni sulla pianificazione fino a quando il carico di elaborazione non risulterà distribuito in modo equo nel server di report.

#### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>Per creare o modificare una pianificazione condivisa (Management Studio)

1.  Avviare [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] e connettersi a un'istanza del server di report.
2.  Espandere il nodo di un server di report in Esplora oggetti.
3.  Fare clic con il pulsante destro del mouse sulla cartella **Pianificazioni condivise** e quindi scegliere **Nuova pianificazione**. Verrà visualizzata la scheda Generale della finestra di dialogo **Nuova pianificazione condivisa** .

     Per modificare una pianificazione condivisa esistente, espandere la cartella Pianificazioni condivise, fare clic con il pulsante destro del mouse sulla pianificazione da modificare e quindi scegliere **Proprietà**.

4.  Digitare un nome descrittivo per la pianificazione.
5.  Selezionare eventualmente la data di inizio della pianificazione. L'impostazione predefinita è il giorno corrente.
6.  Selezionare eventualmente la data di fine della pianificazione. L'esecuzione della pianificazione verrà arrestata da tale data, ma la pianificazione non verrà eliminata.
7.  Per configurare una pianificazione periodica, selezionare **Ora**, **Giorno**, **Settimana**o **Mese**. Verranno visualizzate opzioni aggiuntive. Utilizzare tali opzioni per configurare la frequenza della pianificazione in base all'ora, al giorno, alla settimana o al mese desiderato.

     In alternativa, per specificare una pianificazione non periodica, selezionare **Singola occorrenza**e quindi specificare l'opzione **Ora di inizio**.

8.  Fare clic su **OK**.

##### <a name="to-delete-a-shared-schedule-management-studio"></a>Per eliminare una pianificazione condivisa (Management Studio)

1.  Espandere il nodo di un server di report in Esplora oggetti.
2.  Per verificare che la pianificazione condivisa non sia attualmente usata nei report, espandere la cartella Pianificazioni condivise, fare clic con il pulsante destro del mouse sulla pianificazione e scegliere **Proprietà**.
3. Fare clic sulla scheda **Report** per visualizzare l'elenco dei report che attualmente usano la pianificazione.
Fare clic su **Annulla**.
4.  Espandere la cartella Pianificazioni condivise, fare clic con il pulsante destro del mouse sulla pianificazione da eliminare e quindi scegliere **Elimina**. Verrà visualizzata la finestra di dialogo **Elimina elementi catalogo** .
5.  Fare clic su **OK**.

 Se si elimina una pianificazione condivisa utilizzata da più report e sottoscrizioni, nel server di report vengono create singole pianificazioni per ogni report e sottoscrizione da cui è stata utilizzata in precedenza la pianificazione condivisa. Ogni nuova pianificazione conterrà la data, l'ora e il criterio di occorrenza specificati nella pianificazione condivisa.

##  <a name="bkmk_sharepoint"></a>Creare e gestire le pianificazioni condivise (modalità SharePoint)
 Per creare, modificare o eliminare pianificazioni condivise in un sito di SharePoint, è necessario essere un amministratore del sito.

 È possibile identificare una pianificazione specifica in base al nome descrittivo corrispondente. Se non è specificato alcun nome, verrà creato un nome predefinito basato sulle caratteristiche della pianificazione, ad esempio il criterio di occorrenza o le date e gli orari di esecuzione.

> [!NOTE]
> La creazione di pianificazioni condivise richiede il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.

### <a name="create-shared-schedules-sharepoint-mode"></a>Creare pianificazioni condivise (modalità SharePoint)
1.  Fare clic su **Azioni sito**.
2.  Fare clic su **Impostazioni sito**.
3.  Nella sezione Reporting Services fare clic su **Gestisci pianificazioni condivise**.
4.  Fare clic su **Aggiungi pianificazione** per aprire la pagina Proprietà pianificazione.
5.  Immettere un nome descrittivo per la pianificazione. Nelle pagine di applicazione usate per i report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , tale nome verrà visualizzato negli elenchi a discesa disponibili nelle pagine di definizione delle pianificazioni all'interno del sito. Se possibile, non utilizzare nomi lunghi di difficile lettura. Adottare una convenzione di denominazione che prevede l'indicazione di informazioni descrittive all'inizio del nome.
6.  Specificare una frequenza. Le opzioni di pianificazione visualizzate nella pagina possono essere modificate automaticamente in modo da supportare la frequenza selezionata. Se, ad esempio, si sceglie **Mese**, nella pagina verranno visualizzati i nomi dei singoli mesi.
7.  Definire la pianificazione. Non tutte le combinazioni di pianificazione sono supportate in una singola pianificazione.
8.  Impostare le date di inizio e di fine.
9. Fare clic su **OK**.

### <a name="delete-shared-schedules-sharepoint-mode"></a>Eliminare pianificazioni condivise (modalità SharePoint)
 Tutte le pianificazioni, sia quelle condivise che quelle specifiche dei report, devono essere eliminate manualmente. Se si elimina una pianificazione condivisa attualmente in uso, tutti i riferimenti a tale pianificazione verranno sostituiti con pianificazioni personalizzate non definite, ovvero pianificazioni personalizzate prive di informazioni di data e ora.

1.  Fare clic su **Azioni sito**.
2.  Fare clic su **Impostazioni sito**.
3.  Nella sezione Reporting Services fare clic su **Gestisci pianificazioni condivise**.
4.  Selezionare la pianificazione e fare clic su **Elimina**.


## <a name="see-also"></a>Vedere anche
 [Pianificazioni](../../reporting-services/subscriptions/schedules.md)  
 [Sospendere e riprendere le pianificazioni condivise](../../reporting-services/subscriptions/pause-and-resume-shared-schedules.md)  
 [Memorizzazione dei report nella cache (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [Creare, modificare ed eliminare snapshot nella cronologia dei report](../report-server/create-modify-and-delete-snapshots-in-report-history.md)

