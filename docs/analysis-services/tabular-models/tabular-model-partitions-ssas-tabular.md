---
title: Le partizioni del modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e8fbbfe1aaf7c97a5739768413cdc04644be6a6
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072648"
---
# <a name="tabular-model-partitions"></a>Partizioni di modelli tabulari 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Le partizioni definite per un modello durante la relativa creazione vengono duplicate in un modello distribuito. Una volta distribuite, è possibile gestire tali partizioni e crearne di nuove tramite la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o tramite uno script. In questo argomento vengono descritte le partizioni in un database modello tabulare distribuito. Per altre informazioni sulla creazione e gestione delle partizioni durante la creazione di modelli, vedere [partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Autorizzazioni](#bkmk_permissions)  
  
-   [Elaborare le partizioni](#bkmk_process_partitions)  
  
-   [Elaborazione parallela](#bkmk_parallelProc)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 Un modello di progetto efficace consente di utilizzare le partizioni per eliminare elaborazioni e successivi carichi del processore non necessari nei server Analysis Services assicurando, nel contempo, che i dati vengano elaborati e aggiornati con una frequenza tale da riflettere i dati più recenti dalle origini dati.  
  
 Ad esempio, in un modello tabulare può essere disponibile una tabella Sales in cui sono inclusi i dati di vendita per l'anno fiscale 2011 e tutti gli anni fiscali precedenti. Nella tabella Sales del modello contiene le tre partizioni seguenti:  
  
|Partition|Periodo dei dati|  
|---------------|---------------|  
|Sales2011|Anno fiscale corrente|  
|Sales2010-2001|Anni fiscali 2001, 2002, 2003, 2004, 2005, 2006. 2007, 2008, 2009, 2010|  
|SalesOld|Tutti gli anni fiscali precedenti agli ultimi dieci anni.|  
  
 Poiché i nuovi dati di vendita vengono aggiunti per l'anno fiscale 2011, devono essere elaborati giornalmente in modo da essere riflessi in maniera accurata nell'analisi dei dati di vendita dell'anno fiscale corrente; di conseguenza la partizione Sales2011 viene elaborata ogni notte.  
  
 Non è necessario elaborare i dati della partizione Sales2010-2001 ogni notte; tuttavia, poiché i dati di vendita per i dieci anni fiscali precedenti possono ancora cambiare occasionalmente a causa di restituzioni o modifiche di prodotti, devono comunque essere elaborati regolarmente, ad esempio, in questo caso, ogni mese. I dati della partizione SalesOld non cambiano mai, pertanto vengono elaborati solo annualmente.  
  
 Quando si immette l'anno fiscale 2012, viene aggiunto una nuova partizione Sales2012 alla tabella Sales della modalità. La partizione Sales2011 può essere quindi unita alla partizione Sales2010-2001 e rinominata Sales2011-2002. I dati dell'anno fiscale 2001 vengono eliminati dalla nuova partizione Sales2011-2002 e spostati nella partizione SalesOld. Tutte le partizioni vengono quindi elaborate per riflettere le modifiche.  
  
 Modalità di implementazione di una strategia di partizione per i modelli tabulari dell'organizzazione in gran parte dipenderanno le necessità di elaborazione dei dati di modello specifico e le risorse disponibili.  
  
##  <a name="bkmk_permissions"></a> Permissions  
 Per creare, gestire ed elaborare partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è necessario disporre delle autorizzazioni appropriate di Analysis Services definite in un ruolo di sicurezza. In ogni ruolo di sicurezza è disponibile una delle autorizzazioni seguenti:  
  
|Autorizzazione|Azioni|  
|----------------|-------------|  
|Amministratore|Lettura, elaborazione, creazione, copia, unione, eliminazione|  
|Process|Lettura, elaborazione|  
|Read Only|lettura|  
  
 Per altre informazioni sulla creazione di ruoli durante la creazione di modelli utilizzando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vedere [ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md). Per altre informazioni sulla gestione dei membri del ruolo dei ruoli di modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vedere [ruoli nei modelli tabulari](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
##  <a name="bkmk_parallelProc"></a> Elaborazione parallela  
Analysis Services include l'elaborazione parallela per tabelle con due o più partizioni, aumentando le prestazioni di elaborazione. Per l'elaborazione parallela non sono previste impostazioni di configurazione (vedere le note). Per impostazione predefinita, l'elaborazione parallela viene eseguita quando si elabora la tabella o si selezionano più partizioni per la stessa tabella e processo. È comunque possibile scegliere di elaborare le partizioni della tabella in modo indipendente.  
  
> [!NOTE]  
>  Per specificare se le operazioni di aggiornamento devono essere eseguite in modo sequenziale o parallelo, usare la proprietà **maxParallism** con il comando [Sequence (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/sequence-command-tmsl).

> [!NOTE]  
>  Se viene rilevata una ricodifica, l'elaborazione parallela può causare un maggior utilizzo delle risorse di sistema, perché è necessario interrompere e riavviare più operazioni di partizione con la nuova codifica in parallelo.  
  
##  <a name="bkmk_process_partitions"></a> Elaborare le partizioni  
 Le partizioni possono essere elaborate (aggiornate) indipendentemente dalle altre partizioni usando la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o tramite uno script. L'elaborazione prevede le opzioni seguenti:  
  
|Modalità|Descrizione|  
|----------|-----------------|  
|Elaborazione predefinita|Rileva lo stato di elaborazione di un oggetto partizione ed esegue l'elaborazione necessaria per recapitare oggetti partizione non elaborati o elaborati parzialmente in uno stato di elaborazione completa. Vengono caricati i dati per le tabelle vuote e le partizioni; vengono compilate o ricompilate le gerarchie, le colonne calcolate e le relazioni.|  
|Elaborazione completa|Elabora un oggetto partizione e tutti gli oggetti in esso contenuti. Quando viene eseguita l'elaborazione completa per un oggetto che è stato già elaborato, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono eliminati tutti i dati dell'oggetto, quindi quest'ultimo viene elaborato. Questo tipo di elaborazione è necessario quando è stata apportata una modifica strutturale a un oggetto.|  
|Elaborare dati|Carica i dati in una partizione o in una tabella senza ricompilare le gerarchie o le relazioni oppure ricalcolare le colonne calcolate e le misure.|  
|Elaborazione pulizia|Rimuove tutti i dati da una partizione.|  
|Elaborazione aggiunta|Aggiornare in modo incrementale la partizione con i nuovi dati.|  
  
##  <a name="bkmk_related_tasks"></a> Attività correlate  
  
|Attività|Descrizione|  
|----------|-----------------|  
|[Creare e gestire partizioni di modelli tabulari](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)|Viene descritto come creare e gestire partizioni in un modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|[Elaborare partizioni di modelli tabulari](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)|Viene descritto come elaborare le partizioni in un modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
