---
title: Gestire un'istanza di CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4a563a47500a329a79513afb83aff4f93ebda7e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748263"
---
# <a name="manage-a-cdc-instance"></a>Gestire un'istanza di CDC
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
 Fare clic su questo collegamento per visualizzare la finestra di dialogo Oracle Logging script contenente lo script di registrazione supplementare Oracle. Per informazioni sulle operazioni che è possibile eseguire in questa finestra di dialogo, vedere [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md).  
  
> [!NOTE]  
>  Quando si eseguono gli script di registrazione supplementare, viene visualizzata la finestra di dialogo Oracle Credentials for Running Script in cui immettere un nome utente e una password Oracle validi. Per informazioni su come fornire le credenziali Oracle appropriate, vedere [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md).  
  
 **CDC Instance Deployment Script**  
 Fare clic su questo collegamento per visualizzare la finestra di dialogo CDC Instance Deployment Script in cui viene visualizzato lo script di distribuzione dell'istanza di CDC. Per informazioni su questa finestra di dialogo, vedere [CDC Instance Deployment Script](cdc-instance-deployment-script.md).  
  
 **Proprietà**  
 Fare clic su questo collegamento per aprire l'editor delle proprietà. La configurazione dell'istanza di CDC viene modificata tramite l'editor delle proprietà. Per ulteriori informazioni sulla modifica delle proprietà per un'istanza di CDC, vedere [Edit Instance Properties](edit-instance-properties.md).  
  
 **Schede del visualizzatore**  
  
 Quando si visualizzano le informazioni per l'istanza di CDC, sono disponibili le schede del visualizzatore seguenti. Le informazioni contenute in queste schede sono di sola lettura.  
  
 **Stato**  
 In questa scheda vengono fornite informazioni e statistiche sullo stato corrente dell'istanza di CDC. Sono contenute le informazioni seguenti.  
  
-   **stato**: Un'icona che indica lo stato corrente dell'istanza di CDC. Di seguito vengono descritti gli stati.  
  
    |||  
    |-|-|  
    |![Error](../media/error.gif "Error")|**Error**. L'istanza di Oracle CDC non è in esecuzione perché si è verificato un errore irreversibile. Sono disponibili gli stati secondari seguenti:<br /><br /> **Configurazione errata**: Si è verificato un errore di configurazione che richiede l'intervento manuale.<br /><br /> **Password obbligatoria**: È stata impostata alcuna password per l'istanza di Oracle CDC o la password non è valida.<br /><br /> **Unexpected**. Tutti gli altri errori non reversibili.|  
    |![OK](../media/okay.gif "OK")|**Esecuzione**: L'istanza di CDC è in esecuzione e sta elaborando i record di modifiche. Sono disponibili gli stati secondari seguenti.<br /><br /> **Inattività**: Tutti i record delle modifiche sono stati elaborati e archiviati nelle tabelle delle modifiche di destinazione. Non sono presenti transazioni attive.<br /><br /> **L'elaborazione**: Sono presenti record delle modifiche in fase di processo che non sono ancora stati scritti nelle tabelle delle modifiche.|  
    |![Arresta](../media/stop.gif "Arresta")|**Arrestato**: L'istanza di CDC non è in esecuzione. Lo stato stopped indica che l'istanza di CDC è stata interrotta in modo normale.|  
    |![Paused](../media/paused.gif "Paused")|**In pausa**: L'istanza di CDC è in esecuzione ma l'elaborazione è sospesa a causa di un errore non irreversibile. Sono disponibili gli stati secondari seguenti:<br /><br /> **Disconnesso**: Impossibile stabilire la connessione al database Oracle di origine. L'elaborazione verrà ripresa dopo il ripristino della connessione.<br /><br /> **Archiviazione**: Lo spazio di archiviazione è pieno. L'elaborazione verrà ripresa non appena sarà nuovamente disponibile dello spazio di archiviazione.<br /><br /> **Logger**: Il logger è connesso a Oracle ma non è possibile leggere i log delle transazioni Oracle a causa di un problema temporaneo, ad esempio, un log delle transazioni necessario non è disponibile.|  
  
-   **Stato dettagliato**: Stato secondario corrente.  
  
-   **Messaggio di stato**: Altre informazioni sullo stato corrente.  
  
-   **Timestamp**: L'ora UTC quando ultima lettura dello stato CDC dalla tabella di stato.  
  
-   **Elaborando**: Vengono monitorate le informazioni seguenti in questa sezione.  
  
    -   **Timestamp dell'ultima transazione**: L'ora locale dell'ultima transazione scritta nelle tabelle delle modifiche.  
  
    -   **Ultima modifica apportata timestamp**: L'ora locale della modifica più recente rilevata dall'istanza di Oracle CDC nei log di transazione database Oracle di origine. Vengono fornite informazioni sulla latenza corrente dell'istanza di CDC nella lettura del log delle transazioni Oracle.  
  
    -   **Intestazione del log delle transazioni CN**: Il numero più recente modifica (CN) che è stato letto dal log delle transazioni Oracle.  
  
    -   **Della parte finale del log delle transazioni CN**: Il numero di modifiche per il ripristino o il riavvio dell'istanza di CDC. L'istanza di Oracle CDC verrà riposizionata su questo percorso in caso di riavvio o di qualsiasi altro tipo di errore, incluso il failover del cluster.  
  
    -   **Current CN**: Numero (SCN) rilevata nel database Oracle di origine (non nel log delle transazioni) dell'ultima modifica.  
  
    -   **Le transazioni attive**: Il numero corrente di transazioni Oracle di origine che elaborate dall'istanza di Oracle CDC e non ancora sottoposte a commit/rollback.  
  
    -   **Le transazioni di staging**: Numero corrente origine Oracle di transazioni gestite temporaneamente per la [CDC. xdbcdc_staged_transactions](the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) tabella.  
  
-   **I contatori**: Vengono monitorate le informazioni seguenti in questa sezione.  
  
    -   **Transazioni completate**: Il numero di transazioni completate dopo l'ultima reimpostazione dell'istanza di CDC. Non sono incluse le transazioni che non contengono tabelle di interesse.  
  
    -   **Le modifiche scritte**: Il numero di modifiche scritte in SQL Server tabelle delle modifiche.  
  
 **Oracle**  
 Vengono visualizzate informazioni sull'istanza di CDC e sulla relativa connessione al database Oracle. Questa scheda è di sola lettura. Per modificare queste proprietà, fare clic con il pulsante destro del mouse sull'istanza nel riquadro sinistro e selezionare **Proprietà** oppure scegliere **Proprietà** nel riquadro destro per aprire la finestra di dialogo delle proprietà dell'\<istanza>.  
  
 Per informazioni su queste proprietà e su come modificarle, vedere [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md).  
  
 **Tabelle**  
 Vengono visualizzate informazioni sulle tabelle incluse nell'istanza di CDC. Sono anche disponibili informazioni sulle colonne. Questa scheda è di sola lettura. Per modificare queste proprietà, fare clic con il pulsante destro del mouse sull'istanza nel riquadro sinistro e selezionare **Proprietà** oppure scegliere **Proprietà** nel riquadro destro per aprire la finestra di dialogo delle proprietà dell'\<istanza>.  
  
 Per informazioni su queste proprietà e su come modificarle, vedere [Edit Tables](edit-tables.md).  
  
 **Advanced**  
 Vengono visualizzate le proprietà avanzate per l'istanza di CDC e i valori delle proprietà. Questa scheda è di sola lettura. Per modificare queste proprietà, fare clic con il pulsante destro del mouse sull'istanza nel riquadro sinistro e selezionare **Proprietà** oppure scegliere **Proprietà** nel riquadro destro per aprire la finestra di dialogo delle proprietà dell'\<istanza>.  
  
 Per informazioni su queste proprietà e su come modificarle, vedere [Edit the Advanced Properties](edit-the-advanced-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Procedura di visualizzazione delle proprietà dell'istanza di CDC](how-to-view-the-cdc-instance-properties.md)   
 [Procedura di modifica delle proprietà dell'istanza di CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Utilizzare la New Instance Wizard](use-the-new-instance-wizard.md)  
  
  
