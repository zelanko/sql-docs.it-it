---
title: Form profilo rapido singola tabella (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fefb8e6c4cd29804f28cb2813fe20aba7c70427c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293912"
---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>Form profilo rapido singola tabella (Attività Profiling dati)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la funzionalità **Form profilo rapido singola tabella** per configurare rapidamente l'attività Profiling dati per analizzare una singola tabella o vista tramite impostazioni predefinite.  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="options"></a>Opzioni  
 **Connection**  
 Consente di selezionare una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) per la connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che contiene la tabella o la vista di cui eseguire il profiling.  
  
 **Tabella o vista**  
 Consente di selezionare una tabella o una vista esistente nel database a cui si connette la gestione connessione specificata.  
  
 **Calcolo**  
 Consente di selezionare i profili da calcolare.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Profilo Rapporto di valori Null nella colonna**|Consente di calcolare un profilo Rapporto di valori Null nella colonna utilizzando le impostazioni predefinite per tutte le colonne applicabili nella tabella o nella vista selezionata.<br /><br /> Questo profilo segnala la percentuale di valori Null nella colonna selezionata e consente di identificare eventuali problemi nei dati, ad esempio un rapporto inaspettatamente elevato di valori Null in una colonna. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Rapporto di valori Null nella colonna &#40;attività Profiling dati&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md).|  
|**Profilo Statistiche di colonna**|Consente di calcolare un profilo Statistiche di colonna utilizzando le impostazioni predefinite per tutte le colonne applicabili nella tabella o nella vista selezionata.<br /><br /> Questo profilo segnala le statistiche, ad esempio la deviazione minima, massima, media e standard per le colonne numeriche e la deviazione minima e massima per le colonne di tipo **datetime** . Consente inoltre di identificare eventuali problemi nei dati, ad esempio le date non valide. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Statistiche di colonna &#40;attività Profiling dati&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md).|  
|**Profilo Distribuzione valori di colonna**|Consente di calcolare un profilo Distribuzione valori di colonna utilizzando le impostazioni predefinite per tutte le colonne applicabili nella tabella o nella vista selezionata.<br /><br /> Questo profilo segnala tutti i valori distinct nella colonna selezionata e la percentuale di righe nella tabella rappresentata da ciascun valore. Può inoltre segnalare i valori che rappresentano più percentuali specificate di righe nella tabella. Il profilo consente infine di identificare eventuali problemi nei dati, ad esempio un numero non corretto di valori distinct in una colonna. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Distribuzione valori di colonna &#40;attività Profiling dati&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md).|  
|**Profilo Distribuzione lunghezze di colonna**|Consente di calcolare un profilo Distribuzione lunghezze di colonna utilizzando le impostazioni predefinite per tutte le colonne applicabili nella tabella o nella vista selezionata.<br /><br /> Questo profilo segnala tutte le singole lunghezze dei valori stringa nella colonna selezionata e la percentuale di righe nella tabella rappresentata da ciascuna lunghezza e consente di identificare eventuali problemi nei dati, ad esempio i valori non validi. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Distribuzione lunghezze di colonna &#40;attività Profiling dati&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md).|  
|**Profilo Criteri di ricerca colonna**|Consente di calcolare un profilo Criteri di ricerca colonna utilizzando le impostazioni predefinite per tutte le colonne applicabili nella tabella o nella vista selezionata.<br /><br /> Questo profilo segnala un set di espressioni regolari relative ai valori in una colonna stringa e consente di identificare eventuali problemi nei dati, ad esempio le stringhe non valide. Questo profilo può inoltre indicare espressioni regolari che possono essere utilizzate in futuro per convalidare nuovi valori. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Criteri di ricerca colonna &#40;attività Profiling dati&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md).|  
|**Profilo Chiave candidata**|Consente di calcolare un profilo Chiave candidata per le combinazioni di colonne che includono fino al numero di colonne specificato in **per un massimo di N colonne chiave**.<br /><br /> Questo profilo segnala se una colonna o un set di colonne è adatto per fungere da chiave per la tabella selezionata e consente inoltre di identificare eventuali problemi nei dati, ad esempio i valori duplicati in una possibile colonna chiave. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Chiave candidata &#40;attività Profiling dati&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md).|  
|**per un massimo di N colonne chiave**|Specifica il numero massimo di colonne di cui eseguire il test nelle possibili combinazioni come chiave per la tabella o la vista. Il valore predefinito è 1. Il valore massimo è 1000. Se si imposta tale numero su 3, verranno testate combinazioni di una, due e tre colonne come chiave.|  
|**Profilo Dipendenza funzionale**|Consente di calcolare un profilo Dipendenza funzionale per le combinazioni di colonne determinanti che includono fino al numero di colonne specificato in **per un massimo di N colonne come colonne determinanti**.<br /><br /> Questo profilo segnala la misura in cui i valori in una colonna (colonna dipendente) dipendono dai valori in un'altra colonna o in un set di colonne (colonna determinante) e consente inoltre di identificare eventuali problemi nei dati, ad esempio i valori non validi. Per altre informazioni sulle impostazioni per questo profilo, vedere [Opzioni di Richiesta profilo Dipendenza funzionale &#40;attività Profiling dati&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md).|  
|**per un massimo di N colonne come colonne determinanti**|Specifica il numero massimo di colonne di cui eseguire il test nelle possibili combinazioni come colonne determinanti. Il valore predefinito è 1. Il valore massimo è 1000. Se si imposta questo numero su 2, ad esempio, verranno testate le combinazioni di una o due colonne che rappresentano le colonne determinanti per un'altra colonna (dipendente).|  
  
> [!NOTE]  
>  Il tipo Profilo Inclusione valore non è disponibile in **Form profilo rapido singola tabella**.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
