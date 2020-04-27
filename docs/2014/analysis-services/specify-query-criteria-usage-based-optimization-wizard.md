---
title: Specificare i criteri di query (Ottimizzazione guidata basata sulle informazioni di utilizzo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.specifyquerycriteria.f1
ms.assetid: 3193adc2-af9f-4234-a4cc-dea0c280a724
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41690da6a4a87bf79d411e2b467aeddfa56b5f00
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068217"
---
# <a name="specify-query-criteria-usage-based-optimization-wizard"></a>Impostazione criteri di query (Ottimizzazione guidata basata sulle statistiche di utilizzo)
  Utilizzare la pagina **Impostazione criteri di query** per scegliere una o più opzioni di filtro per identificare le query da ottimizzare.  
  
> [!NOTE]  
>  Se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non riesce a connettersi al log di query, questa pagina non è disponibile.  
  
## <a name="options"></a>Opzioni  
 **Statistiche log di query**  
 Consente di visualizzare informazioni sulle query archiviate nel log di query per le partizioni selezionate. Sono disponibili gli elementi seguenti:  
  
|Termine|Definizione|  
|----------|----------------|  
|**Totale query**|Consente di visualizzare il numero totale di query archiviate nel log di query per le partizioni selezionate.|  
|**Query distinte**|Consente di visualizzare il numero totale di query distinte archiviate nel log di query per le partizioni selezionate.|  
|**Utenti distinti**|Consente di visualizzare il numero totale di utenti distinti associati alle query archiviate nel log di query per le partizioni selezionate.|  
|**Tempo di risposta medio**|Consente di visualizzare i tempi di risposta medi per le query archiviate nel log di query per le partizioni selezionate.|  
  
 **Data di inizio**  
 Consente di filtrare le query del log di query in base a una data e ora di inizio. Selezionare o digitare una data nell'elenco a discesa.  
  
> [!NOTE]  
>  Se l'opzione **Data di fine** non è selezionata, vengono considerate tutte le query del log di query con data e ora corrispondenti o successive a quelle specificate per questa opzione.  
  
 **Data di fine**  
 Consente di filtrare le query del log di query in base a una data e ora di fine. Selezionare o digitare una data nell'elenco a discesa.  
  
> [!NOTE]  
>  Se l'opzione **Data di inizio** non è selezionata, vengono considerate tutte le query del log di query con data e ora corrispondenti o precedenti a quelle specificate per questa opzione.  
  
 **Utenti**  
 Consente di filtrare le query del log di query in base a un set di utenti. Fare clic sul pulsante (**...**) per visualizzare la finestra di dialogo **Selezione utenti** e selezionare gli utenti in base ai quali filtrare le query. Per altre informazioni sulla finestra di dialogo **Selezione utenti**, vedere [Finestra di dialogo Selezione utenti &#40;Analysis Services - Dati multidimensionali&#41;](user-selection-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Query più frequenti**  
 Consente di filtrare le query del log di query in base alla percentuale maggiore di query distinte eseguite più spesso per le partizioni selezionate. Selezionare o digitare un valore percentuale nella casella di testo.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto dell'ottimizzazione guidata basata sull'utilizzo](usage-based-optimization-wizard-f1-help.md)   
 [Procedure guidate di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
