---
title: Concedere le autorizzazioni per stored procedure (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a363336af1bee8c3f84ff620f667c7c0d510b73
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080725"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>Concedere le autorizzazioni per le stored procedure (Analysis Services)
  In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] le stored procedure, o assembly, sono routine esterne, scritte in un linguaggio di programmazione [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET, che estendono le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Gli assembly permettono allo sviluppatore di sfruttare tutte le potenzialità di integrazione tra più linguaggi, gestione delle eccezioni e supporto per il controllo delle versioni, per la distribuzione e per il debug.  
  
 Per registrare un assembly, è necessario essere un amministratore del server. Visualizzare [Concedi autorizzazioni di amministratore del Server &#40;Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="security-context-for-stored-procedure-execution"></a>Contesto di sicurezza per l'esecuzione di stored procedure  
 Una stored procedure può essere chiamata da qualsiasi utente. In base al modo in cui è stata configurata, una stored procedure può essere eseguita nel contesto dell'utente che chiama la procedura o nel contesto di un utente anonimo. Poiché un utente anonimo non dispone di un contesto di sicurezza, utilizzare questa funzionalità quando si configura l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modo da concedere l'accesso anonimo.  
  
 Dopo che l'utente chiama una stored procedure ma prima che [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esegui la stored procedure, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] valuta le azioni all'interno della stored procedure. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] valuta le azioni in una stored procedure in base all'intersezione delle autorizzazioni concesse all'utente e al set di autorizzazioni utilizzato per eseguire la routine. Se la stored procedure contiene un'azione che non può essere eseguita dal ruolo del database a cui appartiene l'utente, l'azione non viene eseguita.  
  
 Di seguito sono indicati i set di autorizzazioni utilizzati per eseguire le stored procedure:  
  
-   **-Safe** set di autorizzazioni con il sicure, una stored procedure non è possibile accedere alle risorse protette nel [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework. Questo set di autorizzazioni consente esclusivamente i calcoli. Si tratta del set di autorizzazioni che offre la protezione maggiore. Le informazioni non vengono propagate al di fuori di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], le autorizzazioni non possono essere innalzate e il rischio di attacchi di manomissione dei dati è ridotto al minimo.  
  
-   **Accesso esterno** set di autorizzazioni con External Access, una stored procedure può accedere alle risorse esterne utilizzando codice gestito. L'impostazione di questo set di autorizzazioni per una stored procedure non causa errori di programmazione che potrebbero portare all'instabilità del server. Questo set di autorizzazioni, tuttavia, potrebbe consentire la propagazione delle informazioni al di fuori del server e potrebbe offrire la possibilità di innalzamento delle autorizzazioni e di attacchi di manomissione dei dati.  
  
-   **Unrestricted** set di autorizzazioni con di senza restrizioni, una stored procedure può accedere alle risorse esterne utilizzando codice. Con questo set di autorizzazioni non vi sono garanzie di sicurezza o di affidabilità per le stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
