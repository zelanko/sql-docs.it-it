---
title: Specificare i criteri di Query (basata sull'utilizzo di ottimizzazione guidata) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.specifyquerycriteria.f1
ms.assetid: 3193adc2-af9f-4234-a4cc-dea0c280a724
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088d53d1257c4b0d4b141b1e090ab1174416d397
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746145"
---
# <a name="specify-query-criteria-usage-based-optimization-wizard"></a>Impostazione criteri di query (Ottimizzazione guidata basata sulle statistiche di utilizzo)
  Utilizzare la pagina **Impostazione criteri di query** per scegliere una o più opzioni di filtro per identificare le query da ottimizzare.  
  
> [!NOTE]  
>  Se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non riesce a connettersi al log di query, questa pagina non è disponibile.  
  
## <a name="options"></a>Opzioni  
 **Statistiche log di query**  
 Consente di visualizzare informazioni sulle query archiviate nel log di query per le partizioni selezionate. Sono disponibili gli elementi seguenti:  
  
|Nome|Definizione|  
|----------|----------------|  
|**Totale query**|Consente di visualizzare il numero totale di query archiviate nel log di query per le partizioni selezionate.|  
|**Query distinte**|Consente di visualizzare il numero totale di query distinte archiviate nel log di query per le partizioni selezionate.|  
|**Utenti distinti**|Consente di visualizzare il numero totale di utenti distinti associati alle query archiviate nel log di query per le partizioni selezionate.|  
|**Tempo medio di risposta**|Consente di visualizzare i tempi di risposta medi per le query archiviate nel log di query per le partizioni selezionate.|  
  
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
  
## <a name="see-also"></a>Vedere anche  
 [F1 Guida della procedura guidata di ottimizzazione basata sull'utilizzo](usage-based-optimization-wizard-f1-help.md)   
 [Procedure guidate di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
