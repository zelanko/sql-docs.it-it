---
title: Editor attività Profiling dati (pagina Richieste profilo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataprofilingtask.profilerequests.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c72acb3d-380e-436e-8041-ed364eddfabd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6deb484f6e213e7089c3aef272ebaebeba13a913
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385589"
---
# <a name="data-profiling-task-editor-profile-requests-page"></a>Data Profiling Task Editor (Profile Requests Page)
  Utilizzare la pagina **Richieste profilo** di **Editor attività Profiling dati** per selezionare e configurare i profili che si desidera calcolare. In una singola attività Profiling dati è possibile calcolare più profili per più colonne o combinazioni di colonne in più tabelle o viste.  
  
 Per altre informazioni sull'uso dell'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](data-profile-viewer.md).  
  
 **Per aprire la pagina Richieste profilo in Editor attività Profiling dati**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente l'attività Profiling dati.  
  
2.  Nella scheda **Flusso di controllo** fare doppio clic sull'attività Profiling dati.  
  
3.  In **Editor attività Profiling dati**fare clic su **Richieste profilo**.  
  
## <a name="using-the-requests-pane"></a>Utilizzo del riquadro delle richieste  
 Il riquadro delle richieste viene visualizzato nella parte superiore della pagina. In questo riquadro sono inclusi tutti i profili configurati per l'attività Profiling dati corrente. Se non è stato configurato alcun profilo, il riquadro delle richieste è vuoto. Per aggiungere un nuovo profilo, fare clic in un'area vuota sotto la colonna **Tipo profilo** e selezionare un tipo di profilo dall'elenco. Per configurare un profilo, selezionare il profilo nel riquadro delle richieste e quindi impostare le proprietà del profilo nel riquadro **Proprietà richiesta** .  
  
### <a name="requests-pane-options"></a>Opzioni del riquadro delle richieste  
 Nel riquadro delle richieste sono disponibili le opzioni seguenti:  
  
 **Visualizza**  
 Consente di specificare se visualizzare tutti i profili configurati per l'attività o solo uno dei profili.  
  
 Le colonne nel riquadro delle richieste cambiano in base all'opzione **Visualizza** selezionata. Per ulteriori informazioni su ognuna di tali colonne, vedere la sezione seguente "Colonne del riquadro delle richieste".  
  
### <a name="requests-pane-columns"></a>Colonne del riquadro delle richieste  
 Le colonne visualizzate nel riquadro delle richieste dipendono dall'opzione **Visualizza** selezionata:  
  
-   Se si sceglie di visualizzare **tutte le richieste**, nel riquadro delle richieste ha due colonne: **Tipo di profilo** e **ID richiesta**.  
  
-   Se si sceglie di visualizzare uno dei cinque profili di colonna, nel riquadro delle richieste presenta quattro colonne: **Tipo di profilo**, **tabella o vista**, **colonna**, e **ID richiesta**.  
  
-   Se si sceglie di visualizzare un profilo chiave candidata, nel riquadro delle richieste presenta quattro colonne: **Tipo di profilo**, **tabella o vista**, **KeyColumns**, e **ID richiesta**.  
  
-   Se si sceglie di visualizzare un profilo dipendenza funzionale, nel riquadro delle richieste ha cinque colonne: **Tipo di profilo**, **tabella o vista**, **colonne determinanti**, **colonna dipendente**, e **ID richiesta**.  
  
-   Se si sceglie di visualizzare un profilo inclusione valore, nel riquadro delle richieste ha sei colonne: **Tipo di profilo**, **Subset tabella o Vista lato**, **tabella o Vista lato Superset**, **colonne lato Subset**, **colonne lato Superset**, e **ID richiesta**.  
  
 Nelle sezioni seguenti vengono descritte tutte le colonne indicate in precedenza.  
  
#### <a name="columns-common-to-all-views"></a>Colonne comuni a tutte le viste  
 **Tipo profilo**  
 Selezionare un profilo dati nelle opzioni seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Richiesta profilo Chiave candidata**|Consente di calcolare un profilo Chiave candidata.<br /><br /> Questo profilo segnala se una colonna o un set di colonne è una chiave, o una chiave approssimativa, per la tabella selezionata. consente inoltre di identificare eventuali problemi nei dati, ad esempio i valori duplicati in una possibile colonna chiave.|  
|**Richiesta profilo Distribuzione lunghezze di colonna**|Consente di calcolare un profilo Distribuzione lunghezze di colonna.<br /><br /> Il profilo Distribuzione lunghezze di colonna segnala tutte le singole lunghezze dei valori stringa nella colonna selezionata e la percentuale di righe nella tabella rappresentata da ogni lunghezza. e consente di identificare eventuali problemi nei dati, ad esempio i valori non validi. Si analizza, ad esempio, una colonna di codici a due caratteri degli stati degli Stati Uniti e si individuano valori con lunghezza maggiore di due caratteri.|  
|**Richiesta profilo Rapporto di valori Null nella colonna**|Consente di calcolare un profilo Rapporto di valori Null nella colonna.<br /><br /> Il profilo Rapporto di valori Null nella colonna segnala la percentuale di valori Null nella colonna selezionata. e consente di identificare eventuali problemi nei dati, ad esempio un rapporto inaspettatamente elevato di valori Null in una colonna. Si analizza, ad esempio, una colonna contenente CAP e si individua una percentuale eccessivamente elevata di codici mancanti.|  
|**Richiesta profilo Criteri di ricerca colonna**|Consente di calcolare un profilo Criteri di ricerca colonna.<br /><br /> Il profilo Criteri di ricerca colonna segnala un set di espressioni regolari che analizzano la percentuale specificata di valori in una colonna stringa. Questo profilo consente di identificare eventuali problemi nei dati, ad esempio le stringhe non valide. Questo profilo può inoltre indicare espressioni regolari che possono essere utilizzate in futuro per convalidare nuovi valori. Un profilo di criteri di ricerca di una colonna contenente CAP, ad esempio, può produrre le espressioni regolari \d{5}-\d{4}, \d{5} e \d{9}. Se vengono visualizzate altre espressioni regolari, è probabile che i dati contengano valori non validi o in formato non corretto.|  
|**Richiesta profilo Statistiche di colonna**|Selezionare questa opzione per calcolare un profilo Statistiche di colonna utilizzando le impostazioni predefinite per tutte le colonne applicabili nella tabella o nella vista selezionata.<br /><br /> Il profilo Statistiche di colonna segnala le statistiche, ad esempio relative a deviazione minima, massima, media e standard, per le colonne numeriche, nonché la deviazione minima e massima per le colonne di tipo `datetime`. Questo profilo consente di identificare eventuali problemi nei dati, ad esempio le date non valide. Si analizza, ad esempio, una colonna di date cronologiche e si individua una data massima successiva alla data corrente.|  
|**Richiesta profilo Distribuzione valori di colonna**|Consente di calcolare un profilo Distribuzione valori di colonna.<br /><br /> Il profilo Distribuzione valori di colonna segnala tutti i valori distinct nella colonna selezionata e la percentuale di righe della tabella rappresentata da ogni valore. Questo profilo può inoltre segnalare i valori che rappresentano più percentuali specificate nella tabella. Il profilo consente infine di identificare eventuali problemi nei dati, ad esempio un numero non corretto di valori distinct in una colonna. Si analizza, ad esempio, una colonna contenente gli stati degli Stati Uniti e si individuano più di 50 valori distinct.|  
|**Richiesta profilo Dipendenza funzionale**|Consente di calcolare un profilo Dipendenza funzionale.<br /><br /> Il profilo Dipendenza funzionale segnala il livello di dipendenza dei valori inclusi in una colonna (colonna dipendente) dai valori presenti in un'altra colonna o set di colonne (colonna determinante). e consente inoltre di identificare eventuali problemi nei dati, ad esempio i valori non validi. Si analizza, ad esempio, la dipendenza tra una colonna contenente i codici postali ZIP (Stati Uniti) e una colonna contenente gli stati degli Stati Uniti. Benché uno stesso codice postale debba essere sempre associato allo stesso stato, il profilo individua alcune violazioni di questa dipendenza.|  
|**Richiesta profilo Inclusione valore**|Consente di calcolare un profilo Inclusione valore.<br /><br /> Il profilo Inclusione valore calcola la sovrapposizione dei valori tra due colonne o set di colonne. Questo profilo può inoltre determinare se una colonna o un set di colonne è adatto a fungere da chiave esterna tra le tabelle selezionate. Il profilo consente infine di identificare eventuali problemi nei dati, ad esempio i valori non validi. Si analizza, ad esempio, la colonna ProductID di una tabella Sales e si individua che la colonna contiene valori non disponibili nella colonna ProductID della tabella Products.|  
  
 **RequestID**  
 Visualizza l'identificatore per la richiesta. Non è in genere necessario modificare il valore generato automaticamente.  
  
#### <a name="columns-common-to-all-individual-profiles"></a>Colonne comuni a tutti i singoli profili  
 **Gestione connessione**  
 Visualizza la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] che stabilisce la connessione al database di origine.  
  
 **ID richiesta**  
 Visualizza un identificatore per la richiesta. Non è in genere necessario modificare il valore generato automaticamente.  
  
#### <a name="columns-common-to-the-five-individual-column-profiles"></a>Colonne comuni ai cinque singoli profili di colonna  
 **Tabella o vista**  
 Visualizza la tabella o la vista che contiene la colonna selezionata.  
  
 **Colonna**  
 Visualizza la colonna selezionata per il profiling.  
  
#### <a name="columns-specific-to-the-candidate-key-profile"></a>Colonne specifiche del profilo Chiave candidata  
 **Tabella o vista**  
 Visualizza la tabella o la vista che contiene le colonne selezionate.  
  
 **Colonne chiave**  
 Visualizza le colonne selezionate per il profiling.  
  
#### <a name="columns-specific-to-the-functional-dependency-profile"></a>Colonne specifiche del profilo Dipendenza funzionale  
 **Tabella o vista**  
 Visualizza la tabella o la vista che contiene le colonne selezionate.  
  
 **Colonne determinanti**  
 Visualizza le colonne selezionate per il profiling come colonna o colonne determinanti. Nell'esempio in cui il codice postale ZIP (Stati Uniti) determina lo stato degli Stati Uniti, la colonna determinante è quella contenente i codici postali.  
  
 **Dependent column**  
 Visualizza le colonne selezionate per il profiling come colonne dipendenti. Nell'esempio in cui il codice postale ZIP (Stati Uniti) determina lo stato degli Stati Uniti, la colonna dipendente è quella contenente gli stati.  
  
#### <a name="columns-specific-to-the-value-inclusion-profile"></a>Colonne specifiche del profilo Inclusione valore  
 **Tabella o vista lato subset**  
 Visualizza la tabella o la vista che contiene la colonna o le colonne selezionate come colonne del lato subset.  
  
 **Tabella o vista lato superset**  
 Visualizza la tabella o la vista che contiene la colonna o le colonne selezionate come colonne del lato superset.  
  
 **Colonne lato subset**  
 Visualizza la colonna o le colonne selezionate per il profiling come colonne del lato subset. Nell'esempio in cui si desidera verificare che i valori presenti in una colonna contenente gli stati degli Stati Uniti siano inclusi in una tabella di riferimento di codici a due caratteri degli stati degli Stati Uniti la colonna del subset è la colonna contenente gli stati della tabella di origine.  
  
 **Colonne lato superset**  
 Visualizza la colonna o le colonne selezionate per il profiling come colonne del lato superset. Nell'esempio in cui si desidera verificare che i valori presenti in una colonna contenente gli stati degli Stati Uniti siano inclusi in una tabella di riferimento di codici a due caratteri degli stati degli Stati Uniti la colonna del superset è la colonna contenente i codici degli stati della tabella di origine.  
  
## <a name="using-the-request-properties-pane"></a>Utilizzo del riquadro Proprietà richiesta  
 Il riquadro **Proprietà richiesta** viene visualizzato al di sotto del riquadro delle richieste. Questo riquadro contiene le opzioni per il profilo selezionato nel riquadro delle richieste.  
  
> [!NOTE]  
>  Dopo avere specificato l'opzione **Tipo profilo**, è necessario selezionare il campo **ID richiesta** per visualizzare le proprietà per la richiesta di profilo nel riquadro **Proprietà richiesta** .  
  
 Queste opzioni variano in base al profilo selezionato. Per informazioni sulle opzioni specifiche per singoli tipi di profilo, vedere gli argomenti seguenti.  
  
-   [Opzioni di Richiesta profilo Chiave candidata &#40;Attività Profiling dati&#41;](candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Rapporto di valori Null nella colonna &#40;Attività Profiling dati&#41;](column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Statistiche di colonna &#40;Attività Profiling dati&#41;](column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Distribuzione valori di colonna &#40;Attività Profiling dati&#41;](column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Distribuzione lunghezze di colonna &#40;Attività Profiling dati&#41;](column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Criteri di ricerca colonna &#40;Attività Profiling dati&#41;](column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Dipendenza funzionale &#40;Attività Profiling dati&#41;](functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [Opzioni di Richiesta profilo Inclusione valore &#40;Attività Profiling dati&#41;](value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
