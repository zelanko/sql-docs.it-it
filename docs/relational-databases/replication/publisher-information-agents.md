---
title: Informazioni sul server di pubblicazione, Agenti | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.commonjobs.f1
ms.assetid: 2346c00d-c269-45a1-af14-68e7fd7ebd7e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: b006eac4981866bbadadaf47bc6d895e3abd0f9e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769726"
---
# <a name="publisher-information-agents"></a>Informazioni sul server di pubblicazione, Agenti
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Nella scheda **Agenti** vengono visualizzate le informazioni sugli agenti e sui processi di manutenzione associati al server di pubblicazione.  
  
-   Agente snapshot, visualizzato per tutte le pubblicazioni.  
  
-   Agente di lettura log, visualizzato per tutte le pubblicazioni transazionali.  
  
-   Agente di lettura coda, visualizzato per le pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda.  
  
-   Processi di manutenzione, visualizzati per tutte le pubblicazioni:  
  
    -   Reinizializzazione delle sottoscrizioni con errori di convalida dei dati  
  
    -   Pulizia del contenuto della cronologia dell'agente: distribuzione  
  
    -   Aggiornamento del monitoraggio della replica per la distribuzione  
  
    -   Controllo degli agenti di replica  
  
    -   Pulizia riferimenti distribuzione: distribuzione  
  
    -   Pulizia dei riferimenti alle sottoscrizioni scaduti  
  
 Per altre informazioni su questi processi, vedere [Amministrazione dell'agente di replica](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
## <a name="options"></a>Opzioni  
 Per visualizzare le informazioni su un agente o su un processo, scegliere l'elemento desiderato dal menu a discesa relativo ai **tipi di agente e processo**. Per ulteriori informazioni e per conoscere le attività correlate a un agente o a un processo, fare clic con il pulsante destro del mouse sulla riga dell'agente o del processo, quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne**.  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne**.  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro**.  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 Nelle sezioni seguenti sono descritti i dati visualizzati in questa scheda per ogni agente o processo.  
  
### <a name="snapshot-agent"></a>agente snapshot  
 **Stato**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Riprova  
  
-   In esecuzione  
  
-   Completato  
  
 **Pubblicazione**  
 Nome della pubblicazione a cui è associato l'agente.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Durata**  
 Quantità di tempo di esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e il tempo totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
 **Frequenza recapito**  
 Frequenza, in comandi al secondo, con cui viene eseguito il commit dei comandi di inizializzazione nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **N. transazioni**  
 Numero di transazioni di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **N. comandi**  
 Numero di comandi di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente. Un comando è equivalente a una modifica dei dati, ad esempio un aggiornamento.  
  
### <a name="log-reader-agent"></a>Agente di lettura log  
 **Stato**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Riprova  
  
-   In esecuzione  
  
-   Non in esecuzione  
  
 **Database di pubblicazione**  
 Nome della pubblicazione a cui è associato l'agente.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Durata**  
 Quantità di tempo di esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e il tempo totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
 **Frequenza recapito**  
 Frequenza, in comandi al secondo, con cui viene eseguito il commit delle modifiche nel database di distribuzione.  
  
 **Latenza**  
 Quantità di tempo, in secondi, trascorsa tra il commit della modifica più recente nel database di pubblicazione e il commit del comando corrispondente nel database di distribuzione.  
  
 **N. transazioni**  
 Numero di transazioni di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **N. comandi**  
 Numero di comandi di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente. Un comando è equivalente a una modifica dei dati, ad esempio un aggiornamento.  
  
 **Media n. comandi**  
 Numero medio di comandi per transazione durante la più recente esecuzione dell'agente.  
  
### <a name="queue-reader-agent"></a>Agente di lettura coda  
 **Stato**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Riprova  
  
-   In esecuzione  
  
-   Non in esecuzione  
  
 **Database di distribuzione**  
 Nome del database di distribuzione a cui è associato l'agente.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Durata**  
 Quantità di tempo di esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
 **Frequenza recapito**  
 Frequenza, in comandi al secondo, con cui viene eseguito il commit delle modifiche nel database di distribuzione.  
  
 **Latenza**  
 Quantità di tempo, in secondi, trascorsa tra il commit della modifica più recente in un database di sottoscrizione e il commit del comando corrispondente nel database di pubblicazione.  
  
 **N. transazioni**  
 Numero di transazioni di cui è stato eseguito il commit nel database di pubblicazione durante la più recente esecuzione dell'agente.  
  
 **N. comandi**  
 Numero di comandi di cui è stato eseguito il commit nel database di pubblicazione durante la più recente esecuzione dell'agente. Un comando è equivalente a una modifica dei dati, ad esempio un aggiornamento.  
  
 **Media n. comandi**  
 Numero medio di comandi per transazione durante la più recente esecuzione dell'agente.  
  
### <a name="maintenance-jobs"></a>Processi di manutenzione  
 **Stato**  
 Stato di ogni processo. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Riprova  
  
-   In esecuzione  
  
-   Non in esecuzione  
  
 **Processo**  
 Nome del processo.  
  
 **Ultima ora inizio**  
 Ultima ora di inizio del processo.  
  
 **Durata**  
 Tempo di esecuzione del processo. Il valore di durata rappresenta il tempo trascorso se il processo è ancora in esecuzione e la durata totale se il processo è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione del processo.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
