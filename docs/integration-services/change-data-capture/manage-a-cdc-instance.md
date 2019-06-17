---
title: Gestire un'istanza di CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5d988854d3dcf63b1a6be85d672fb2af31d6620
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728718"
---
# <a name="manage-a-cdc-instance"></a>Gestire un'istanza di CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile utilizzare CDC Designer Console per visualizzare le informazioni relative alle istanze create e per gestire l'operazione delle istanze.  
  
 Fare clic sul nome di un'istanza nel riquadro sinistro per visualizzare le relative informazioni.  
  
> [!NOTE]  
>  Se si seleziona un servizio nel riquadro sinistro, l'elenco delle istanze disponibili viene visualizzato al centro di CDC Designer Console. Se si seleziona una delle istanze in questa sezione, è possibile eseguire le attività nel riquadro destro. Non è tuttavia possibile visualizzare le informazioni nelle schede delle proprietà.  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>Operazioni possibili quando si visualizzano le informazioni sull'istanza di CDC  
 Dal riquadro destro vengono eseguite le azioni seguenti:  
  
 **Start**  
 Fare clic su **Start** per avviare l'acquisizione delle modifiche per l'istanza di CDC selezionata.  
  
 **Arresta**  
 Fare clic su **Stop** per arrestare l'acquisizione delle modifiche per l'istanza di CDC selezionata. Quando si arresta l'istanza di CDC, le modifiche acquisite fino a quel momento non vanno perse e verranno recapitate alla ripresa dell'istanza di CDC.  
  
 **Reimposta**  
 Fare clic su **Reset** per reimpostare l'istanza di CDC sullo stato iniziale (vuoto). Questa opzione diventa disponibile dopo che l'istanza di CDC è stata interrotta. Tutte le modifiche presenti nelle tabelle delle modifiche e lo stato interno dell'istanza di CDC vengono eliminati. Al successivo avvio dell'istanza di CDC, l'acquisizione delle modifiche verrà avviata da quel momento e includerà solo le transazioni avviate dopo l'avvio dell'istanza di CDC.  
  
 Scegliere **OK** nella finestra di dialogo di conferma per reimpostare l'istanza di CDC ed eliminare le modifiche scritte nelle tabelle delle modifiche.  
  
 **Elimina**  
 Scegliere **Delete** per eliminare in modo definitivo l'istanza di CDC. Questa opzione diventa disponibile dopo che l'istanza di CDC viene arrestata.  
  
 Scegliere **OK** nella finestra di dialogo di conferma per eliminare l'istanza di CDC.  
  
 **Oracle Logging Script**  
 Fare clic su questo collegamento per visualizzare la finestra di dialogo Oracle Logging script contenente lo script di registrazione supplementare Oracle. Per informazioni sulle operazioni che è possibile eseguire in questa finestra di dialogo, vedere [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md).  
  
> [!NOTE]  
>  Quando si eseguono gli script di registrazione supplementare, viene visualizzata la finestra di dialogo Oracle Credentials for Running Script in cui immettere un nome utente e una password Oracle validi. Per informazioni su come fornire le credenziali Oracle appropriate, vedere [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md).  
  
 **CDC Instance Deployment Script**  
 Fare clic su questo collegamento per visualizzare la finestra di dialogo CDC Instance Deployment Script in cui viene visualizzato lo script di distribuzione dell'istanza di CDC. Per informazioni su questa finestra di dialogo, vedere [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md).  
  
 **Proprietà**  
 Fare clic su questo collegamento per aprire l'editor delle proprietà. La configurazione dell'istanza di CDC viene modificata tramite l'editor delle proprietà. Per ulteriori informazioni sulla modifica delle proprietà per un'istanza di CDC, vedere [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md).  
  
 **Schede del visualizzatore**  
  
 Quando si visualizzano le informazioni per l'istanza di CDC, sono disponibili le schede del visualizzatore seguenti. Le informazioni contenute in queste schede sono di sola lettura.  
  
 **Stato**  
 In questa scheda vengono fornite informazioni e statistiche sullo stato corrente dell'istanza di CDC. Sono contenute le informazioni seguenti.  
  
-   **Stato**: icona che indica lo stato corrente dell'istanza di CDC. Di seguito vengono descritti gli stati.  
  
    |||  
    |-|-|  
    |![Error](../../integration-services/change-data-capture/media/error.gif "Error")|**Error**. L'istanza di Oracle CDC non è in esecuzione perché si è verificato un errore irreversibile. Sono disponibili gli stati secondari seguenti:<br /><br /> **Misconfigured** (Configurazione non valida): si è verificato un errore di configurazione che richiede l'intervento manuale.<br /><br /> **Password Required** (Password obbligatoria): nessuna password impostata per l'istanza di Oracle CDC oppure la password non è valida.<br /><br /> **Unexpected**. Tutti gli altri errori non reversibili.|  
    |![OK](../../integration-services/change-data-capture/media/okay.gif "OK")|**In esecuzione**: l'istanza di CDC è in esecuzione ed è in corso l'elaborazione dei record delle modifiche. Sono disponibili gli stati secondari seguenti:<br /><br /> **Idle** (Inattivo): tutti i record delle modifiche sono stati elaborati e archiviati nelle tabelle delle modifiche di destinazione. Non sono presenti transazioni attive.<br /><br /> **Processing** (Elaborazione in corso): è in corso l'elaborazione di alcuni record delle modifiche che non sono ancora stati scritti nelle tabelle delle modifiche.|  
    |![Arresta](../../integration-services/change-data-capture/media/stop.gif "Arresta")|**Arrestato**: L'istanza di CDC non è in esecuzione. Lo stato stopped indica che l'istanza di CDC è stata interrotta in modo normale.|  
    |![Paused](../../integration-services/change-data-capture/media/paused.gif "Paused")|**Paused** (Sospeso): l'istanza di CDC è in esecuzione ma l'elaborazione è stata sospesa in seguito a un errore non irreversibile. Sono disponibili gli stati secondari seguenti:<br /><br /> **Disconnected** (Disconnesso): non è possibile stabilire la connessione al database Oracle di origine. L'elaborazione verrà ripresa dopo il ripristino della connessione.<br /><br /> **Storage** (Archiviazione): lo spazio di archiviazione è esaurito. L'elaborazione verrà ripresa non appena sarà nuovamente disponibile dello spazio di archiviazione.<br /><br /> **Logger**: il logger è connesso a Oracle ma non è in grado di leggere i log delle transazioni Oracle a causa di un problema temporaneo, ad esempio un log delle transazioni necessario non è disponibile.|  
  
-   **Detailed Status** (Stato dettagliato): stato secondario corrente.  
  
-   **Status Message** (Messaggio di stato): ulteriori informazioni sullo stato corrente.  
  
-   **Timestamp**: ora UTC dell'ultima lettura dello stato di CDC dalla tabella di stato.  
  
-   **Currently Processing** (Elaborazione in corso): vengono monitorate le informazioni seguenti in questa sezione.  
  
    -   **Last transaction timestamp** (Timestamp ultima transazione): ora locale dell'ultima transazione scritta nelle tabelle relative alle modifiche.  
  
    -   **Last change timestamp** (Timestamp ultima modifica): ora locale della modifica più recente rilevata dall'istanza di Oracle CDC nei log delle transazioni del database Oracle di origine. Vengono fornite informazioni sulla latenza corrente dell'istanza di CDC nella lettura del log delle transazioni Oracle.  
  
    -   **Transaction log head CN** (Numero modifica inizio log transazioni): numero della modifica più recente letto dal log delle transazioni Oracle.  
  
    -   **Transaction log tail CN** (Numero modifica fine log transazioni): numero della modifica per il recupero o il riavvio dell'istanza di CDC. L'istanza di Oracle CDC verrà riposizionata su questo percorso in caso di riavvio o di qualsiasi altro tipo di errore, incluso il failover del cluster.  
  
    -   **Current CN** (Numero modifica corrente): numero dell'ultima modifica rilevata nel database Oracle di origine, non nel log delle transazioni.  
  
    -   **Active transactions** (Transazioni attive): numero corrente di transazioni Oracle di origine elaborate dall'istanza di Oracle CDC e non ancora sottoposte a commit o a rollback.  
  
    -   **Staged transactions** (Transazioni con gestione temporanea): numero corrente di transazioni Oracle di origine con gestione temporanea nella tabella [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions).  
  
-   **Counters** (Contatori): vengono monitorate le informazioni seguenti in questa sezione.  
  
    -   **Completed transactions** (Transazioni completate): numero di transazioni completate dopo l'ultima reimpostazione dell'istanza di CDC. Non sono incluse le transazioni che non contengono tabelle di interesse.  
  
    -   **Written changes** (Modifiche scritte): numero di modifiche scritte nelle tabelle delle modifiche di SQL Server.  
  
 **Oracle**  
 Vengono visualizzate informazioni sull'istanza di CDC e sulla relativa connessione al database Oracle. Questa scheda è di sola lettura. Per modificare queste proprietà, fare clic con il pulsante destro del mouse sull'istanza nel riquadro sinistro e selezionare **Proprietà** oppure scegliere **Proprietà** nel riquadro destro per aprire la finestra di dialogo delle proprietà dell'\<istanza>.  
  
 Per informazioni su queste proprietà e su come modificarle, vedere [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md).  
  
 **Tabelle**  
 Vengono visualizzate informazioni sulle tabelle incluse nell'istanza di CDC. Sono anche disponibili informazioni sulle colonne. Questa scheda è di sola lettura. Per modificare queste proprietà, fare clic con il pulsante destro del mouse sull'istanza nel riquadro sinistro e selezionare **Proprietà** oppure scegliere **Proprietà** nel riquadro destro per aprire la finestra di dialogo delle proprietà dell'\<istanza>.  
  
 Per informazioni su queste proprietà e su come modificarle, vedere [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
 **Advanced**  
 Vengono visualizzate le proprietà avanzate per l'istanza di CDC e i valori delle proprietà. Questa scheda è di sola lettura. Per modificare queste proprietà, fare clic con il pulsante destro del mouse sull'istanza nel riquadro sinistro e selezionare **Proprietà** oppure scegliere **Proprietà** nel riquadro destro per aprire la finestra di dialogo delle proprietà dell'\<istanza>.  
  
 Per informazioni su queste proprietà e su come modificarle, vedere [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Procedura di visualizzazione delle proprietà dell'istanza di CDC](../../integration-services/change-data-capture/how-to-view-the-cdc-instance-properties.md)   
 [Procedura di modifica delle proprietà dell'istanza di CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Utilizzare la New Instance Wizard](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
