---
title: Funzionalità disattivate per impostazione predefinita (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59c27d5f34d6e5a3f33e0f153a9077995bd99650
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080015"
---
# <a name="features-off-by-default-analysis-services"></a>Funzionalità disabilitate per impostazione predefinita (Analysis Services)
  Un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è progettata per garantire sicurezza per impostazione predefinita. Le funzionalità che potrebbero mettere a repentaglio la sicurezza sono pertanto disabilitate per impostazione predefinita. Le funzionalità seguenti sono installate in stato disabilitato e devono essere abilitate specificamente se si desidera usarle.  
  
## <a name="feature-list"></a>Elenco di funzionalità  
 Per abilitare le funzionalità seguenti, connettersi a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Fare clic con il pulsante destro del mouse sul nome dell'istanza e scegliere **Facet**. In alternativa, è possibile abilitare queste funzionalità tramite le proprietà del server, come illustrato nella sezione seguente.  
  
-   Query di data mining ad hoc (OpenRowset)  
  
-   Oggetti collegati (a)  
  
-   Oggetti collegati (da)  
  
-   Ascolto solo su connessioni locali  
  
-   Funzioni definite dall'utente  
  
## <a name="server-properties"></a>Proprietà server  
 Le funzionalità aggiuntive disattivate per impostazione predefinita possono essere abilitate tramite le proprietà del server. Connettersi a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Fare clic con il pulsante destro del mouse sul nome dell'istanza e scegliere **Proprietà**. Fare clic su **Generale**, quindi su **Mostra avanzate** per visualizzare un elenco più ampio di proprietà.  
  
-   Query di data mining ad hoc (OpenRowset)  
  
-   Consenti modelli di data mining di sessione (Data Mining)  
  
-   Oggetti collegati (a)  
  
-   Oggetti collegati (da)  
  
-   Funzioni definite dall'utente basate su COM  
  
-   Definizioni di traccia Flight Recorder (modelli).  
  
-   Registrazione query  
  
-   Ascolto solo su connessioni locali  
  
-   XML binario  
  
-   Compressione  
  
-   Affinità gruppo. Per informazioni dettagliate, vedere [Thread Pool Properties](../server-properties/thread-pool-properties.md) .  
  
  
