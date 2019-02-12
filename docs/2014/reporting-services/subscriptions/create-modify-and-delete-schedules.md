---
title: Creare, modificare ed eliminare pianificazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 231fbf5211654d126f09ceb048501c7b2eacf0c3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039582"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  In questo argomento vengono fornite informazioni sulla creazione, la modifica e l'eliminazione di pianificazioni.  
  
 Contenuto dell'argomento:  
  
-   [Panoramica della gestione di pianificazioni condivise](#bkmk_overview)  
  
-   [Creare e gestire pianificazioni condivise (modalità SharePoint)](#bkmk_sharepoint)  
  
-   [Creare e gestire pianificazioni condivise (modalità nativa)](#bkmk_native)  
  
##  <a name="bkmk_overview"></a> Panoramica della gestione di pianificazioni condivise  
 Per gestire le pianificazioni condivise per la modalità nativa, utilizzare la pagina Pianificazioni in Gestione report o la cartella Pianificazioni condivise in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per la modalità SharePoint, utilizzare le pagine di gestione per l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 È possibile visualizzare tutte le pianificazioni condivise definite per il server di report, sospenderle e riprenderle (solo in Gestione report) e selezionare le pianificazioni da modificare o eliminare. Nella pagina Pianificazioni condivise, per ogni pianificazione è disponibile un riepilogo delle informazioni seguenti: frequenza, proprietario, data di scadenza e stato.  
  
 È possibile stabilire se una pianificazione condivisa è utilizzata in modo mediante le operazioni seguenti:  
  
-   Controllo dei valori nei campi relativi allo stato e alla data dell'ultima esecuzione o di quella successiva nella pagina Pianificazioni condivise. Se una pianificazione non viene più eseguita perché è scaduta, nel campo Stato viene visualizzata la data di scadenza.  
  
-   Visualizzazione della pagina Report di una determinata pianificazione condivisa. In questa pagina vengono elencati tutti i report e i set di dati condivisi che utilizzano la pianificazione condivisa.  
  
-   Visualizzazione dei file dei log di esecuzione o dei log di traccia del report per verificare se i report sono stati eseguiti negli orari specificati nella pianificazione. Per altre informazioni, vedere [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
##  <a name="bkmk_sharepoint"></a> Creare e gestire le pianificazioni condivise (modalità SharePoint)  
 Una pianificazione condivisa rappresenta una pianificazione multifunzionale che fornisce informazioni di pianificazione pronte per l'utilizzo a qualsiasi numero di report o sottoscrizioni. È possibile creare una pianificazione condivisa una sola volta e quindi farvi riferimento in una pagina di sottoscrizione o delle proprietà quando sono necessarie informazioni di pianificazione. Le pianificazioni condivise possono essere gestite, sospese e riprese a livello centralizzato. Per evitare l'esecuzione di un report o una sottoscrizione, è invece necessario modificare manualmente una pianificazione personalizzata.  
  
 Per creare, modificare o eliminare pianificazioni condivise in un sito di SharePoint, è necessario essere un amministratore del sito.  
  
 È possibile identificare una pianificazione specifica in base al nome descrittivo corrispondente. Se non è specificato alcun nome, verrà creato un nome predefinito basato sulle caratteristiche della pianificazione, ad esempio il criterio di occorrenza o le date e gli orari di esecuzione.  
  
> [!NOTE]  
>  La creazione di pianificazioni condivise richiede il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
### <a name="create-shared-schedules-sharepoint"></a>Creare pianificazioni condivise (SharePoint)  
  
##### <a name="to-create-shared-schedules"></a>Per creare pianificazioni condivise  
  
1.  Fare clic su **Azioni sito**.  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  Nella sezione Reporting Services fare clic su **Gestisci pianificazioni condivise**.  
  
4.  Fare clic su **Aggiungi pianificazione** per aprire la pagina Proprietà pianificazione.  
  
5.  Immettere un nome descrittivo per la pianificazione. Nelle pagine di applicazione usate per i report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , tale nome verrà visualizzato negli elenchi a discesa disponibili nelle pagine di definizione delle pianificazioni all'interno del sito. Se possibile, non utilizzare nomi lunghi di difficile lettura. Adottare una convenzione di denominazione che prevede l'indicazione di informazioni descrittive all'inizio del nome.  
  
6.  Specificare una frequenza. Le opzioni di pianificazione visualizzate nella pagina possono essere modificate automaticamente in modo da supportare la frequenza selezionata. Se, ad esempio, si sceglie **Mese**, nella pagina verranno visualizzati i nomi dei singoli mesi.  
  
7.  Definire la pianificazione. Non tutte le combinazioni di pianificazione sono supportate in una singola pianificazione.  
  
8.  Impostare le date di inizio e di fine.  
  
9. Scegliere **OK**.  
  
### <a name="delete-shared-schedules-sharepoint"></a>Eliminare pianificazioni condivise (SharePoint)  
 Tutte le pianificazioni, sia quelle condivise che quelle specifiche dei report, devono essere eliminate manualmente. Se si elimina una pianificazione condivisa attualmente in uso, tutti i riferimenti a tale pianificazione verranno sostituiti con pianificazioni personalizzate non definite, ovvero pianificazioni personalizzate prive di informazioni di data e ora.  
  
 Eliminare una pianificazione e farla scadere sono due operazioni diverse. La data di scadenza viene impostata per arrestare una pianificazione, non per eliminarla. Dato che le pianificazioni vengono utilizzate per l'automatizzazione delle operazioni del server di report, non vengono mai eliminate automaticamente. Le pianificazioni scadute possono essere utilizzate dagli amministratori del server di report come riscontro per individuare la causa dell'improvviso arresto di un processo automatico. Un amministratore del server di report che non controlla innanzitutto se la pianificazione è scaduta potrebbe eseguire una diagnosi errata del problema oppure perdere inutilmente tempo tentando di risolvere i problemi di un processo che invece è perfettamente funzionante.  
  
 Una pianificazione personalizzata rimane associata al report anche se scaduta. È possibile determinare se una pianificazione è scaduta verificandone la data di fine. Una pianificazione condivisa scaduta rimane comunque nell'elenco Pianificazioni condivise. Il campo Stato indica se la pianificazione è scaduta. È possibile riattivare la pianificazione posticipando la data di fine oppure rimuovere il riferimento alla pianificazione se non è più necessario.  
  
##### <a name="to-delete-a-shared-schedule"></a>Per eliminare una pianificazione condivisa  
  
1.  Fare clic su **Azioni sito**.  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  Nella sezione Reporting Services fare clic su **Gestisci pianificazioni condivise**.  
  
4.  Selezionare la pianificazione e fare clic su **Elimina**.  
  
##  <a name="bkmk_native"></a> Creare e gestire pianificazioni condivise (modalità nativa)  
 Le pianificazioni condivise devono essere eliminate manualmente utilizzando la pagina Pianificazioni in Gestione report o la cartella Pianificazioni condivise in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Se si elimina una pianificazione condivisa in uso, tutti i riferimenti a essa verranno sostituiti con pianificazioni in base al report.  
  
 I report e le pianificazioni specifiche della sottoscrizione vengono eliminati quando si elimina il report o la sottoscrizione o quando si sceglie un approccio diverso per eseguire il report o la sottoscrizione. Se ad esempio si sceglie **Esegui sempre il report con i dati più recenti** , verrà eliminata una pianificazione in base al report creata per eseguire un report come snapshot dell'esecuzione del report stesso.  
  
 Eliminare una pianificazione e farla scadere sono due operazioni diverse. La data di scadenza viene impostata per arrestare una pianificazione, non per eliminarla. Dato che le pianificazioni vengono utilizzate per l'automatizzazione di numerose funzionalità, non vengono mai eliminate automaticamente. Le pianificazioni scadute possono essere utilizzate dagli amministratori del server di report come riscontro per individuare la causa dell'improvviso arresto di un processo automatico. Un amministratore del server di report che non controlla innanzitutto se la pianificazione è scaduta potrebbe eseguire una diagnosi errata del problema oppure perdere inutilmente tempo a cercare di risolvere i problemi di un processo che invece è perfettamente funzionante.  
  
 Una pianificazione in base al report rimane associata al report anche se scaduta. È possibile determinare se una pianificazione è scaduta verificandone la data di fine. Le pianificazioni condivise scadute rimangono comunque nell'elenco della pagina Pianificazioni condivise. Il campo Stato indica se la pianificazione è scaduta. È possibile riattivare la pianificazione posticipando la data di fine oppure rimuovere il riferimento alla pianificazione se non è più necessario.  
  
### <a name="create-delete-or-modify-a-shared-schedule-report-manager"></a>Creare, eliminare o modificare una pianificazione condivisa (Gestione report)  
 Le operazioni di creazione e modifica di una pianificazione consistono nell'impostazione delle opzioni di frequenza che determinano quando deve essere eseguita la pianificazione.  
  
-   Le pianificazioni condivise vengono create come elementi distinti. Dopo che sono state create, è possibile farvi riferimento nel contesto della definizione di una sottoscrizione o di un'altra operazione pianificata.  
  
-   Le pianificazioni in base al report vengono create quando si definisce una sottoscrizione o si impostano le proprietà di esecuzione dei report. L'impostazione delle informazioni di pianificazione fa parte del processo di definizione di una sottoscrizione o di impostazione di proprietà. Per definire una pianificazione in base al report, è necessario aprire il report o la sottoscrizione che la utilizzerà.  
  
 In una pianificazione condivisa sono contenute le informazioni sulla pianificazione e sull'occorrenza che possono essere utilizzate da qualsiasi numero di sottoscrizioni e report pubblicati in esecuzione in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se il numero di report e sottoscrizioni in esecuzione contemporaneamente è elevato, è possibile creare una pianificazione condivisa per tali processi. Se si desidera modificare successivamente il criterio di occorrenza o la data di fine, è possibile apportare la modifica in un unico punto.  
  
 Le pianificazioni condivise sono più semplici da gestire e consentono una maggiore flessibilità nella gestione di operazioni pianificate. È possibile ad esempio sospendere e quindi riprendere una pianificazione condivisa. Inoltre, se si rileva che sono in esecuzione contemporaneamente troppe operazioni pianificate, sarà possibile creare più pianificazioni condivise per eseguirle in orari diversi, quindi modificare le informazioni sulla pianificazione fino a quando il carico di elaborazione non risulterà distribuito in modo equo nel server di report.  
  
 Le pianificazioni possono essere create o modificate in qualsiasi momento. Tuttavia, se l'esecuzione di una pianificazione inizia prima del completamento delle modifiche, verrà utilizzata la versione precedente della pianificazione. La pianificazione modificata ha effetto solo dopo essere stata salvata.  
  
 Se si decide di modificare una pianificazione condivisa, è possibile sospenderla prima di iniziare ad apportarvi le modifiche. Le modifiche avranno effetto quando la pianificazione verrà ripresa.  
  
##### <a name="to-create-or-modify-a-shared-schedule-report-manager"></a>Per creare o modificare una pianificazione condivisa (Gestione report)  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report fare clic su **Impostazioni sito**sulla barra degli strumenti principale.  
  
3.  Fare clic su **Pianificazioni**.  
  
4.  Fare clic su **Nuova pianificazione**. Per modificare una pianificazione esistente, fare clic sul nome della pianificazione.  
  
5.  Digitare un nome descrittivo per la pianificazione.  
  
6.  Selezionare **Ora**, **Giorno**, **Settimana**o **Mese**. Fare clic su **Singola occorrenza** per creare una pianificazione eseguita una sola volta. Dopo aver specificato le impostazioni di base della pianificazione, verranno visualizzate ulteriori opzioni.  
  
7.  Selezionare eventualmente la data di inizio della pianificazione. L'impostazione predefinita è il giorno corrente. È possibile posticipare la data di inizio della pianificazione scegliendo una data successiva.  
  
8.  Selezionare facoltativamente una data di fine della pianificazione. L'esecuzione della pianificazione verrà arrestata da tale data, ma la pianificazione non verrà eliminata.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-report-manager"></a>Per eliminare una pianificazione condivisa (Gestione report)  
  
1.  In Gestione report fare clic su **Impostazioni sito**sulla barra degli strumenti principale.  
  
    > [!NOTE]  
    >  Se **Impostazioni sito** non è disponibile, non si dispone dell'autorizzazione di accesso alle impostazioni del sito.  
  
2.  Nella sezione **Altro** della pagina fare clic su **Gestisci pianificazioni condivise**.  
  
3.  Selezionare la casella di controllo accanto alla pianificazione che si desidera eliminare e quindi fare clic su **Elimina**.  
  
 Se si elimina una pianificazione condivisa utilizzata da più report e sottoscrizioni, nel server di report vengono create singole pianificazioni per ogni report e sottoscrizione da cui è stata utilizzata in precedenza la pianificazione condivisa. Ogni nuova pianificazione conterrà la data, l'ora e il criterio di occorrenza specificati nella pianificazione condivisa. Si noti che in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è disponibile una funzionalità di gestione centrale delle singole pianificazioni. Se si elimina una pianificazione condivisa, sarà necessario gestire le informazioni sulla pianificazione per ogni elemento singolo.  
  
 Se non si è certi se viene utilizzata una pianificazione condivisa, eliminarla in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] invece. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] sono disponibili le stesse funzionalità di gestione delle pianificazioni condivise di Gestione report, ma è presente inoltre una pagina Report aggiuntiva contenente il nome di ogni report in cui viene utilizzata la pianificazione.  
  
### <a name="create-delete-or-modify-a-shared-schedule-management-studio"></a>Creare, eliminare o modificare una pianificazione condivisa (Management Studio)  
 In una pianificazione condivisa sono contenute le informazioni sulla pianificazione e sull'occorrenza che possono essere utilizzate da qualsiasi numero di sottoscrizioni e report pubblicati in esecuzione in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se il numero di report e sottoscrizioni in esecuzione contemporaneamente è elevato, è possibile creare una pianificazione condivisa per tali processi. Se si desidera modificare successivamente il criterio di occorrenza o la data di fine, è possibile apportare la modifica in un unico punto.  
  
 Le pianificazioni condivise sono più semplici da gestire e consentono una maggiore flessibilità nella gestione di operazioni pianificate. È possibile ad esempio sospendere e quindi riprendere una pianificazione condivisa. Inoltre, se si rileva che sono in esecuzione contemporaneamente troppe operazioni pianificate, sarà possibile creare più pianificazioni condivise per eseguirle in orari diversi, quindi modificare le informazioni sulla pianificazione fino a quando il carico di elaborazione non risulterà distribuito in modo equo nel server di report.  
  
##### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>Per creare o modificare una pianificazione condivisa (Management Studio)  
  
1.  Avviare SQL Server Management Studio e connettersi a un'istanza del server di report.  
  
2.  Espandere il nodo di un server di report in Esplora oggetti.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella Pianificazioni condivise, quindi scegliere **Nuova pianificazione**. Verrà visualizzata la scheda Generale della finestra di dialogo **Nuova pianificazione condivisa** .  
  
     Per modificare una pianificazione condivisa esistente, espandere la cartella Pianificazioni condivise, fare clic con il pulsante destro del mouse sulla pianificazione da modificare e quindi scegliere **Proprietà**.  
  
4.  Digitare un nome descrittivo per la pianificazione.  
  
5.  Selezionare eventualmente la data di inizio della pianificazione. L'impostazione predefinita è il giorno corrente.  
  
6.  Selezionare eventualmente la data di fine della pianificazione. L'esecuzione della pianificazione verrà arrestata da tale data, ma la pianificazione non verrà eliminata.  
  
7.  Per configurare una pianificazione periodica, selezionare **Ora**, **Giorno**, **Settimana**o **Mese**. Verranno visualizzate opzioni aggiuntive. Utilizzare tali opzioni per configurare la frequenza della pianificazione in base all'ora, al giorno, alla settimana o al mese desiderato.  
  
     In alternativa, per specificare una pianificazione non periodica, selezionare **Singola occorrenza**e quindi specificare l'opzione **Ora di inizio**.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-management-studio"></a>Per eliminare una pianificazione condivisa (Management Studio)  
  
1.  Espandere il nodo di un server di report in Esplora oggetti.  
  
2.  Espandere la cartella Pianificazioni condivise, fare clic con il pulsante destro del mouse sulla pianificazione da eliminare, quindi scegliere **Elimina**. Verrà visualizzata la finestra di dialogo **Elimina elementi catalogo** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Se si elimina una pianificazione condivisa utilizzata da più report e sottoscrizioni, nel server di report vengono create singole pianificazioni per ogni report e sottoscrizione da cui è stata utilizzata in precedenza la pianificazione condivisa. Ogni nuova pianificazione conterrà la data, l'ora e il criterio di occorrenza specificati nella pianificazione condivisa. Si noti che in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è disponibile una funzionalità di gestione centrale delle singole pianificazioni. Se si elimina una pianificazione condivisa, sarà necessario gestire le informazioni sulla pianificazione per ogni elemento singolo. Prima di eliminare una pianificazione condivisa, utilizzare la pagina [Report](../tools/schedule-properties-reports-page.md) per verificare i report che la utilizzano attualmente.  
  
## <a name="see-also"></a>Vedere anche  
 [Schedules](schedules.md)   
 [Pause and Resume Shared Schedules](pause-and-resume-shared-schedules.md)   
 [Memorizzare nella cache un report &#40;Gestione report&#41;](../report-server/cache-a-report-report-manager.md)   
 [Aggiungere uno snapshot alla cronologia del report &#40;Gestione report&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)  
  
  
