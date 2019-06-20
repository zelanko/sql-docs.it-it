---
title: Risolvere i problemi di elaborazione dei dati (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 678f523c-e181-4456-9a54-7b7bf044b8d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f76d67d5e44fc700d4b889840ef2dcc07a0bfde0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065772"
---
# <a name="troubleshoot-process-data-ssas-tabular"></a>Risolvere i problemi relativi all'elaborazione dei dati (SSAS tabulare)
  In questo argomento vengono fornite informazioni sull'elaborazione (aggiornamento) dei dati del modello quando si crea un modello tramite [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Non sono disponibili informazioni sull'elaborazione di dati in modelli distribuiti in un'istanza del server Analysis Services. Per altre informazioni sull'elaborazione dei dati in un modello distribuito, vedere [Creare script per le attività amministrative in Analysis Services](script-administrative-tasks-in-analysis-services.md).  
  
 Sezioni dell'argomento:  
  
-   [Funzionamento dell'elaborazione dei dati](#bkmk_how_df_works)  
  
-   [Impatto dell'elaborazione dei dati](#bkmk_impact_of_df)  
  
-   [Determinazione dell'origine dei dati](#bkmk_det_source)  
  
-   [Come stabilire la data dell'ultimo aggiornamento dei dati](#bkmk_det_last_ref)  
  
-   [Restrizioni sulle origini dati aggiornabili](#bkmk_restrictions)  
  
-   [Restrizioni delle modifiche a un'origine dati](#bkmk_rest_changes)  
  
##  <a name="bkmk_how_df_works"></a> Funzionamento dell'elaborazione dei dati  
 Quando si elaborano i dati, questi vengono sostituiti con nuovi dati in Progettazione modelli. Non è possibile importare solo le nuove righe di dati o solo i dati modificati. In Progettazione modelli non si tiene traccia delle righe aggiunte precedentemente.  
  
 L'elaborazione di dati si verifica come una transazione, ovvero può essere completata interamente o non esserla affatto. Non è previsto un aggiornamento parziale dei dati.  
  
 L'elaborazione manuale dei dati, che viene avviata da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], viene gestita dall'istanza in memoria locale di Analysis Services. L'operazione di elaborazione dei dati può quindi influire sulle prestazioni di altre attività in esecuzione nel computer. Se tuttavia si pianifica l'elaborazione automatica dei dati in un modello distribuito tramite uno script, l'istanza di Analysis Services gestisce il processo di importazione e il relativo intervallo.  
  
##  <a name="bkmk_impact_of_df"></a> Impatto dell'elaborazione dei dati  
 Un'elaborazione dei dati comporta di solito un ricalcolo dei dati.  Mediante l'elaborazione dei dati si ottengono i dati più recenti dalle origini esterne. Per ricalcolo si intende l'aggiornamento del risultato di tutte le formule che utilizzano i dati che sono stati modificati. Un'operazione di elaborazione generalmente comporta l'attivazione del ricalcolo.  
  
 Per questo motivo, è necessario tenere conto del potenziale impatto e delle possibili conseguenze prima di modificare le origini dati o di elaborare i dati ottenuti dall'origine dati.  
  
-   Dopo aver apportato modifiche all'origine dati, è possibile che alcune parti dei dati del modello risultino interrotte. Se non è possibile recuperare tutte le colonne dall'origine dati, ad esempio se sono state eliminate o modificate, l'elaborazione non verrà completata e sarà necessario aggiornare i mapping tra i dati di origine e quelli del modello. Per altre informazioni, vedere [Modificare una connessione all'origine dati esistente &#40;SSAS tabulare&#41;](edit-an-existing-data-source-connection-ssas-tabular.md).  
  
-   Dopo l'elaborazione, alcune colonne potrebbero essere contrassegnate come contenenti un errore. Questa situazione può verificarsi se la formula DAX nella colonna utilizza dati che non erano più disponibili al momento dell'elaborazione o il cui tipo è stato modificato oppure se ai dati esterni è stato aggiunto un valore non valido. Per risolvere il problema, è possibile modificare la formula o eliminare la colonna, se è basata su dati che non sono più disponibili.  
  
-   Le formule che utilizzano dati aggiornati dovranno essere ricalcolate. Il tempo necessario per eseguire questa operazione dipende dalle dimensioni del modello.  
  
-   Se nel modello sono contenute più origini dati, potrebbe essere necessario elaborare l'intero modello (Elabora tutto), anche se è stata modificata una sola origine dati esterna. Ad esempio, se si creano misure basate sulle colonne calcolate e per tali colonne vengono utilizzati valori di altre colonne calcolate, Progettazione modelli consente innanzitutto di analizzare le dipendenze, quindi di elaborare in ordine l'intera catena di oggetti correlati. Il tempo richiesto per l'esecuzione di questa operazione dipende dalla complessità delle dipendenze.  
  
-   Quando si modifica un filtro, è necessario ricalcolare l'intero modello.  
  
##  <a name="bkmk_det_source"></a> Determinazione dell'origine dei dati  
 In caso di dubbi sulla provenienza dei dati del modello, è possibile visualizzare i dettagli, inclusi il nome e il percorso del file di origine, utilizzando gli strumenti disponibili in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] .  
  
#### <a name="to-find-the-source-of-existing-data"></a>Per individuare l'origine dei dati esistenti  
  
1.  In Progettazione modelli selezionare la tabella contenente i dati per cui si desidera conoscere l'origine.  
  
2.  Fare clic sul menu **Tabella** , quindi scegliere **Proprietà tabella**.  
  
3.  Nella finestra di dialogo **Modifica proprietà tabella** prendere nota del valore elencato per **Nome connessione**.  
  
4.  Nel menu [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]Modello **in** fare clic su **Connessioni esistenti**.  
  
5.  Nella finestra di dialogo **Connessioni esistenti** selezionare l'origine dati con il nome annotato al passaggio 3 e fare clic su **Modifica**.  
  
6.  Nella finestra di dialogo **Modifica connessioni** visualizzare le informazioni di connessione, quali il nome del database, il percorso del file o il percorso del report.  
  
##  <a name="bkmk_det_last_ref"></a> Come stabilire la data dell'ultimo aggiornamento dei dati  
 È possibile stabilire la data dell'ultimo aggiornamento dei dati utilizzando Proprietà tabella.  
  
#### <a name="to-find-the-date-and-time-that-a-table-was-last-processed"></a>Per individuare la data e l'ora dell'ultima elaborazione della tabella  
  
1.  In Progettazione modelli selezionare la tabella contenente i dati di cui si desidera conoscere la data di aggiornamento.  
  
2.  Fare clic sul menu **Tabella** , quindi scegliere **Proprietà tabella**.  
  
3.  In **Ultimo aggiornamento** della finestra di dialogo **Modifica proprietà tabella** viene indicata la data dell'ultimo aggiornamento della tabella.  
  
##  <a name="bkmk_restrictions"></a> Restrizioni sulle origini dati aggiornabili  
 Vengono applicate alcune restrizioni alle origini dati che possono essere elaborate automaticamente da un modello distribuito in un'istanza di Analysis Services. Assicurarsi di selezionare solo le origini dati che soddisfano i criteri seguenti:  
  
-   L'origine dati deve essere disponibile quando si verifica l'elaborazione dei dati e nel percorso dichiarato. Se l'origine dati iniziale si trova in un'unità disco locale dell'utente che ha creato il modello, è necessario escludere tale origine dati dall'operazione di elaborazione dei dati o individuare un modo per pubblicare tale origine dati in un percorso accessibile tramite una connessione di rete. Se si sposta un'origine dati in un percorso della rete, assicurarsi di aprire il modello in Progettazione modelli e di ripetere i passaggi di recupero dei dati. Tale operazione è necessaria per riattivare le informazioni di connessione archiviate nelle proprietà di connessione dell'origine dati.  
  
-   L'accesso all'origine dati deve essere eseguito utilizzando le credenziali incorporate nella connessione all'origine dati. Le credenziali incorporate vengono create nella connessione all'origine dati quando ci si connette all'origine dati esterna.  
  
-   L'elaborazione dei dati deve avere un esito positivo per tutte le origini dati specificate. In caso contrario, i dati elaborati vengono rimossi e viene mantenuta l'ultima versione salvata del modello. Escludere tutte le origini dati di cui non si è sicuri.  
  
-   L'elaborazione dei dati non deve invalidare altri dati del modello. Quando si elabora un subset di dati, è importante capire se il modello è ancora valido una volta che i dati più recenti vengono aggregati con i dati statici che non derivano dallo stesso periodo di tempo. In qualità di responsabile della progettazione di modelli, l'utente deve conoscere le dipendenze dei propri dati e assicurarsi che l'elaborazione dei dati sia adatta per il modello.  
  
     L'accesso a un'origine dati esterna viene eseguito tramite una stringa di connessione incorporata, un URL o un percorso UNC specificati quando i dati originali sono stati importati nel modello tramite l'Importazione guidata tabella. Le informazioni di connessione originali archiviate nella connessione all'origine dati vengono riutilizzate per le successive operazioni di aggiornamento dei dati. Non sono disponibili informazioni di connessione distinte create e gestite per l'elaborazione dei dati. Vengono utilizzate solo le informazioni di connessione esistenti.  
  
##  <a name="bkmk_rest_changes"></a> Restrizioni delle modifiche a un'origine dati  
 Esistono alcune restrizioni relativamente alle modifiche che è possibile apportare a un'origine dati:  
  
-   I tipi di dati di una colonna possono essere modificati solo in un tipo di dati compatibile. Ad esempio, se nei dati della colonna sono inclusi i numeri decimali, non è possibile modificare il tipo di dati in numeri interi. Tuttavia, è possibile impostare i dati numerici su testo. Per altre informazioni sui tipi di dati, vedere [Tipi di dati supportati &#40;SSAS tabulare&#41;](tabular-models/data-types-supported-ssas-tabular.md).  
  
-   Non è possibile selezionare più colonne in tabelle diverse e modificarne le proprietà. È possibile utilizzare una sola tabella o vista alla volta.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborare manualmente i dati &#40;SSAS tabulare&#41;](manually-process-data-ssas-tabular.md)   
 [Modificare una connessione all'origine dati esistente &#40;SSAS tabulare&#41;](edit-an-existing-data-source-connection-ssas-tabular.md)  
  
  
