---
title: Partizioni di modelli tabulari (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.partitions.partitionmgr.imbi.f1
ms.assetid: 041c269f-a229-4a41-8794-6ba4b014ef83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aaa2b608665e50b25b39d78a39a57bb08b55cf31
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066390"
---
# <a name="tabular-model-partitions-ssas-tabular"></a>Partizioni di modelli tabulari (SSAS tabulare)
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Le partizioni definite per un modello durante la relativa creazione vengono duplicate in un modello distribuito. Una volta distribuite, è possibile gestire tali partizioni e crearne di nuove tramite la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o tramite uno script. In questo argomento vengono descritte le partizioni in un database modello tabulare distribuito. Per altre informazioni sulla creazione e sulla gestione di partizioni durante la creazione di un modello, vedere [Partizioni &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md).  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Autorizzazioni](#bkmk_permissions)  
  
-   [Elaborare le partizioni](#bkmk_process_partitions)  
  
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
  
##  <a name="bkmk_permissions"></a> Autorizzazioni  
 Per creare, gestire ed elaborare partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è necessario disporre delle autorizzazioni appropriate di Analysis Services definite in un ruolo di sicurezza. In ogni ruolo di sicurezza è disponibile una delle autorizzazioni seguenti:  
  
|Autorizzazione|Azioni|  
|----------------|-------------|  
|Amministratore|Lettura, elaborazione, creazione, copia, unione, eliminazione|  
|Process|Lettura, elaborazione|  
|Read Only|lettura|  
  
 Per altre informazioni sulla creazione di ruoli durante la generazione di modelli tramite [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vedere [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md). Per altre informazioni sulla gestione dei membri dei ruoli del modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vedere [Ruoli nei modelli tabulari &#40;SSAS tabulare&#41;](tabular-model-roles-ssas-tabular.md).  
  
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
|[Creare e gestire partizioni di modelli tabulari &#40;SSAS tabulare&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)|Viene descritto come creare e gestire partizioni in un modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|[Elaborare partizioni di modelli tabulari &#40;SSAS tabulare&#41;](process-tabular-model-partitions-ssas-tabular.md)|Viene descritto come elaborare le partizioni in un modello tabulare distribuito tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
