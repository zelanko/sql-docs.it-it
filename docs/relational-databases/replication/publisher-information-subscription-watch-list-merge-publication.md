---
title: Scheda Elenco verifica sottoscrizioni (merge - SSMS)
description: Informazioni sulla scheda "Elenco verifica sottoscrizioni" di Monitoraggio replica in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f44c8b3762b7abae0e79ec213812f5dc31b52ac9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716753"
---
# <a name="publisher-information-subscription-watch-list-merge-publication"></a>Informazioni sul server di pubblicazione, Elenco verifica sottoscrizioni (pubblicazione di tipo merge)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La scheda **Elenco verifica sottoscrizioni** è disponibile per i server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive e consente di visualizzare le informazioni sulle sottoscrizioni da tutte le pubblicazioni disponibili nel server di pubblicazione selezionato. È possibile filtrare l'elenco delle sottoscrizioni per visualizzare errori, avvisi ed eventuali sottoscrizioni con prestazioni scarse. Questa scheda offre gli amministratori un unico punto per il monitoraggio di tutte le attività di replica eseguite nel server di pubblicazione. Monitoraggio replica visualizza infatti tutte le sottoscrizioni che necessitano di attenzione in base al tipo di replica selezionato e all'opzione scelta nell'elenco a discesa **Mostra** . Poiché gli elementi visualizzati in questa scheda si basano sullo stato e le prestazioni correnti, le sottoscrizioni vengono visualizzate in questa pagina solo se queste corrispondono all'opzione selezionata nella casella di riepilogo **Mostra** .  
  
## <a name="options"></a>Opzioni  
 Per ulteriori informazioni su una sottoscrizione e sulle attività correlate, fare clic con il pulsante destro del mouse sulla riga della sottoscrizione e quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne** .  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne** .  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro** .  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Mostra sottoscrizioni di tipo merge**  
 Consente di selezionare il tipo di sottoscrizioni (transazionali, snapshot o merge) da visualizzare per il server di distribuzione selezionato.  
  
 **Mostra**  
 Consente di selezionare gli stati della sottoscrizione da visualizzare per il tipo di sottoscrizione selezionato. Ad esempio, è possibile scegliere di visualizzare solo le sottoscrizioni con errori.  
  
 **Status**  
 Stato di ogni sottoscrizione, determinato dallo stato dell'agente di merge.  
  
 Per impostazione predefinita, la griglia contenente le informazioni sulla sottoscrizione viene ordinata in base alla colonna **Stato** e quindi ordinata in base alla colonna **Prestazioni** per le sottoscrizioni che hanno lo stesso stato. Nell'elenco seguente vengono indicati i valori di stato possibili e l'ordinamento di tali valori, ad esempio gli errori vengono sempre visualizzati nella parte superiore della griglia.  
  
-   Errore  
  
-   Prestazioni critiche  
  
-   Merge con esecuzione prolungata  
  
-   Scadenza imminente/Scaduta  
  
-   Sottoscrizione non inizializzata  
  
-   Ripetizione comando non riuscito  
  
-   Sincronizzazione in corso  
  
-   Non in sincronizzazione  
  
 L'ordinamento determina inoltre il valore da visualizzare quando per una particolare sottoscrizione sono disponibili più stati. Se, ad esempio, per una sottoscrizione sono presenti errori e la scadenza della sottoscrizione è imminente, nella colonna **Stato** sarà visualizzato il valore **Errore**.  
  
 I valori di stato **Prestazioni critiche**, **Merge con esecuzione prolungata**, **Scadenza imminente/Scaduta**e **Sottoscrizione non inizializzata** sono avvisi. Se viene visualizzato un avviso, nella colonna **Stato** viene inoltre indicato se un agente è in corso di sincronizzazione. Ad esempio, lo stato potrebbe essere **Sincronizzazione in corso, Prestazioni critiche**.  
  
 I valori di stato **Scadenza imminente/Scaduta** e **Merge con esecuzione prolungata** possono essere visualizzati solo se sono impostati i valore soglia. Il valore di stato **Prestazioni critiche** può essere visualizzato solo dopo cinque sincronizzazioni di sottoscrizioni con lo stesso tipo di connessione (remota o LAN). Per informazioni sulle misurazioni delle prestazioni e sull'impostazione dei valori soglia, vedere [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) e [Impostare valori di soglia e avvisi in Monitoraggio replica](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Sottoscrizione**  
 Nome di ogni sottoscrizione nel formato:*SubscriberName: SubscriptionDatabaseName*.  
  
 **Nome descrittivo**  
 Descrizione di ogni sottoscrizione. La descrizione può essere immessa nella finestra di dialogo **Proprietà sottoscrizione** oppure può essere specificata tramite il parametro `@description` di [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) o [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Gli utenti utilizzano spesso la descrizione come "nome descrittivo" o come nome alternativo per la sottoscrizione.  
  
 **Pubblicazione**  
 Nome della pubblicazione con cui viene sincronizzata una sottoscrizione nel formato: *PublicationDatabaseName: PublicationName*.  
  
 **Prestazioni**  
 Valutazione delle prestazioni per ogni sottoscrizione, basata sulle misurazioni più recenti della frequenza di recapito rilevate da Monitoraggio replica. La valutazione è determinata dal confronto tra le prestazioni delle singole sottoscrizioni e le prestazioni medie passate delle sottoscrizioni della pubblicazione che utilizzano lo stesso tipo di connessione (remota o LAN). In Monitoraggio replica viene visualizzato un valore dopo cinque sincronizzazioni con 50 o più modifiche eseguite con lo stesso tipo di connessione. Se sono state eseguite meno di 5 sincronizzazioni con almeno 50 modifiche oppure durante la sincronizzazione più recente sono state apportate meno di 50 modifiche, la colonna è vuota.  
  
> [!NOTE]  
>  Le prestazioni sono basate sul tipo di connessione visualizzato nella colonna **Connessione** . È pertanto possibile che una sottoscrizione con una frequenza di recapito inferiore visualizzi una valutazione delle prestazioni migliore di un'altra sottoscrizione se la prima sottoscrizione viene sincronizzata tramite una connessione più lenta.  
  
 La valutazione delle prestazioni può corrispondere a uno dei valori seguenti:  
  
-   Eccellenti  
  
-   Buone  
  
-   Discrete  
  
-   Scarse  
  
 Per altre informazioni sulla modalità con cui vengono definite le valutazioni delle prestazioni e impostati i valori soglia per le prestazione, vedere [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Frequenza recapito**  
 Numero di righe elaborate al secondo dall'agente di merge.  
  
 **Ultima sincronizzazione**  
 Ora dell'ultima esecuzione dell'agente di merge. Durante tale sincronizzazione le modifiche potrebbero essere state elaborate o meno. Se la sincronizzazione è in corso viene visualizzato un valore di percentuale di completamento.  
  
 **Duration**  
 Tempo di esecuzione dell'agente di merge durante l'ultima sincronizzazione. Il valore di durata rappresenta il tempo trascorso se l'agente di merge è ancora in sincronizzazione e la durata totale se l'agente di merge ha eseguito la sincronizzazione in precedenza.  
  
 **Connection**  
 Tipo di connessione tra il Sottoscrittore e il server di pubblicazione. I valori possibili sono **LAN**, **Remota**e **Internet**. Il valore **Internet** viene visualizzato se la sottoscrizione utilizza la sincronizzazione tramite il Web.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Sincronizzazione Web per la replica di tipo merge](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
