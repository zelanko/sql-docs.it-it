---
title: Definizione conversione valuta (configurazione guidata funzionalità di Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.existingscriptpage.f1
ms.assetid: 37dd65b7-9d8d-44ad-b316-96a92c622472
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b463363e2e239c348c626cf1ef1d61e621877814
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082147"
---
# <a name="define-currency-conversion-business-intelligence-wizard"></a>Definizione conversione valuta (Configurazione guidata funzionalità di Business Intelligence)
  Usare la pagina **Definizione conversione valuta** per esaminare lo script MDX (Multidimensional Expressions) contenente la funzionalità di conversione valuta generata dalla Configurazione guidata funzionalità di Business Intelligence. Sarà quindi possibile sovrascrivere la funzionalità di conversione valuta precedentemente definita nello script MDX del cubo con lo script MDX generato dalla procedura guidata o accodare il nuovo script a quello esistente.  
  
> [!NOTE]  
>  Questa pagina verrà visualizzata solo se la Configurazione guidata funzionalità di Business Intelligence rileva almeno una conversione valuta precedentemente definita nello script MDX per il cubo. Nello script MDX per un cubo, le conversioni valuta sono racchiuse tra i commenti seguenti:  
>   
>  `//<Currency conversion>`  
>   
>  `...`  
>   
>  `[MDX statements for the currency conversion]`  
>   
>  `...`  
>   
>  `//</Currency conversion>`  
>   
>  Se questi commenti vengono modificati o eliminati, la Configurazione guidata funzionalità di Business Intelligence può non essere in grado di rilevare le conversioni valuta precedentemente definite.  
  
## <a name="options"></a>Opzioni  
 **Nuovo script di conversione valuta**  
 Consente di visualizzare lo script MDX generato dalla sessione corrente della Configurazione guidata funzionalità di Business Intelligence.  
  
 **Sovrascrivi script di conversione valuta esistente**  
 Selezionare questa opzione per sovrascrivere lo script MDX visualizzato in **Script di conversione valuta esistente** con lo script MDX visualizzato in **Nuovo script di conversione valuta**.  
  
 **Accoda dopo**  
 Selezionare questa opzione per accodare lo script MDX visualizzato in **Nuovo script di conversione valuta** alla fine dello script MDX visualizzato in **Script di conversione valuta esistente**. Lo script accodato viene visualizzato come nuova sezione.  
  
 **Script di conversione valuta esistente**  
 Consente di selezionare la sezione dello script MDX esistente che contiene la funzionalità di conversione valuta precedentemente definita da sovrascrivere o a cui accodare il nuovo script.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto della configurazione guidata funzionalità di Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Progettazione cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Progettazione dimensioni &#40;Analysis Services-Dati multidimensionali&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
