---
title: Configurazione attributi dimensione (configurazione guidata Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.acctintelligence.selectattributes.f1
ms.assetid: 3d046e63-bcb1-4ab1-9c37-652463fa68c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5fe43b53878744586c3d0d8ec5719d6241b0a302
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087452"
---
# <a name="configure-dimension-attributes-business-intelligence-wizard"></a>Configurazione attributi dimensione (Configurazione guidata funzionalità di Business Intelligence)
  Utilizzare la pagina **Configurazione attributi dimensione** per eseguire il mapping tra gli attributi di dimensione e i tipi di attributo utilizzati da [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per identificare gli attributi per le dimensioni di tipo Conto.  
  
## <a name="options"></a>Opzioni  
 **Tipo di dimensione**  
 Consente di visualizzare il tipo di dimensione selezionato.  
  
> [!NOTE]  
>  Questa opzione non è disponibile perché il `Type` proprietà della dimensione non può essere impostata su un valore diverso da *Account* per le dimensioni dell'account.  
  
 **Attributi della dimensione**  
 Consente di visualizzare i tipi di attributo validi di cui è possibile eseguire il mapping agli attributi della dimensione esistenti.  
  
 **Include**  
 Selezionare una casella di controllo per includere nella dimensione il tipo di attributo corrispondente.  
  
 **Tipo di attributo**  
 Consente di visualizzare i tipi di attributo di cui è possibile eseguire il mapping agli attributi della dimensione esistenti.  
  
 **Attributo della dimensione**  
 Consente di selezionare l'attributo della dimensione di cui è necessario eseguire il mapping al tipo di attributo corrispondente.  
  
 **Imposta misure semiadditive in base al tipo di account**  
 Selezionare questa opzione per modificare ogni misura associata alla dimensione corrente da aggregare in base al tipo di conto.  
  
> [!NOTE]  
>  Questa opzione non viene visualizzata se la Configurazione guidata funzionalità di Business Intelligence è stata avviata da Progettazione dimensioni oppure facendo clic con il pulsante destro del mouse su una dimensione in Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della Configurazione guidata funzionalità di Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Finestra di progettazione del cubo &#40;Analysis Services - dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Finestra di progettazione della dimensione &#40;Analysis Services - dati multidimensionali&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
