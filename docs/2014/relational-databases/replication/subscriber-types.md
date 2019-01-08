---
title: Tipi di Sottoscrittore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e34d70b84e20f8c4f65e09baad9d8388aa96fca3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806213"
---
# <a name="subscriber-types"></a>Tipi di Sottoscrittore
  La replica di tipo merge consente di specificare i tipi di Sottoscrittore che si richiede vengano supportati da una pubblicazione. La selezione dei tipi di Sottoscrittore causa l'impostazione del *livello di compatibilità della pubblicazione*, che determina le funzionalità utilizzabili da una pubblicazione.  
  
 Dopo aver creato una pubblicazione snapshot, è possibile aumentare il livello di compatibilità della pubblicazione, rendendolo più restrittivo, nella pagina **Generale** della finestra di dialogo **Proprietà pubblicazione** . Non è possibile diminuire il livello di compatibilità.  
  
## <a name="options"></a>Opzioni  
 Consente di selezionare i tipi di Sottoscrittore che devono essere supportati dalla pubblicazione.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 La pubblicazione è in grado di utilizzare tutte le funzionalità.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 La pubblicazione richiede che i file di snapshot siano in formato carattere, gestito automaticamente dall'agente snapshot. [!INCLUDE[ssEW](../../includes/ssew-md.md)] prevede inoltre alcune limitazioni non correlate al livello di compatibilità.  
  
 Se si seleziona questa opzione, l'opzione per la sincronizzazione Web viene abilitata per la pubblicazione. Per ulteriori informazioni sulla sincronizzazione Web, vedere [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)   
 [Riferimento alle proprietà &#40;replica&#41;](properties-reference-replication.md)  
  
  
