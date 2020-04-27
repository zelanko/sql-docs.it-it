---
title: Selezione tabelle e viste (creazione guidata vista origine dati) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.selecttablesandviews.f1
ms.assetid: ea7d1232-f213-46e9-90d9-0fd616ca003d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4b940d5cb3c91cc8257ef1a3e6828286bc1c240
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069245"
---
# <a name="select-tables-and-views-data-source-view-wizard-analysis-services"></a>Selezione tabelle e viste (Creazione guidata vista origine dati) (Analysis Services)
  La pagina **Selezione tabelle e viste** consente di selezionare le tabelle o le viste dall'origine dati da includere nella vista origine dati.  
  
## <a name="options"></a>Opzioni  
 **Available objects**  
 Elenca le tabelle e le viste nello schema dell'origine dei dati. Se è presente più di uno schema, il nome dello schema viene anteposto al nome dei singoli oggetti. Se è presente un solo schema, ai nomi degli oggetti non verrà anteposto il nome dello schema.  
  
 Per riordinare l'elenco in ordine crescente o decrescente, fare clic su **Nome** o **Tipo**.  
  
 **Included objects**  
 Elenca le tabelle e le viste nella vista origine dati.  
  
 Per riordinare l'elenco in ordine crescente o decrescente, fare clic su **Nome** o **Tipo**.  
  
 **Filter**  
 Filtra gli oggetti elencati in **Oggetti disponibili**. Digitare una stringa e quindi fare clic su **Filtro** per elencare solo i nomi che contengono la stringa specificata. Per ricercare una stringa esatta di caratteri, racchiudere la stringa tra virgolette doppie. Il filtro non supporta la distinzione tra maiuscole e minuscole.  
  
 È possibile includere i caratteri jolly inclusi nella tabella seguente in qualsiasi punto della stringa di filtro.  
  
|Carattere jolly|valore|  
|------------------------|-----------|  
|**\***|Qualsiasi stringa di caratteri|  
|**%**|Qualsiasi stringa di caratteri|  
|**?**|Un singolo carattere|  
|**"** *stringa* **"**|Una stringa letterale di caratteri. Questo carattere jolly corrisponderà a qualsiasi sottostringa nel nome dell'oggetto.|  
  
 **Show system objects**  
 Mostra gli oggetti di sistema in **Oggetti disponibili**. Questa opzione è disponibile solo se il provider dell'origine dei dati espone gli oggetti di sistema. Se si rimuove un oggetto di sistema dall'elenco **Oggetti inclusi** , questa opzione viene automaticamente selezionata.  
  
 **Add related tables**  
 Aggiunge tutte le tabelle correlate a quelle elencate in **Oggetti inclusi**. Questa opzione non consente di aggiungere visualizzazioni, bensì permette di aggiungere tabelle partizionate. Se si seleziona un criterio di corrispondenza dei nomi nella pagina **Corrispondenza nomi** della procedura guidata, questa opzione include anche le tabelle logicamente correlate in base al criterio selezionato. Vengono inoltre incluse le tabelle correlate a nuove tabelle correlate aggiunte e quelle che presentano una struttura identica alla tabella originale.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto della creazione guidata vista origine dati &#40;Analysis Services&#41;](data-source-view-wizard-f1-help-analysis-services.md)   
 [Viste origine dati in modelli multidimensionali](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
