---
title: Progettazione di Stored procedure | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a617df9d88bde17c08fb4d2235ad751a5609e2d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181093"
---
# <a name="designing-stored-procedures"></a>Progettazione di stored procedure
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sia il modello a oggetti amministrativo AMO (Analysis Management Objects) sia il modello a oggetti orientato al client [!INCLUDE[msCoName](../../includes/msconame-md.md)] ADO MD (ActiveX® Data Objects Multidimensional) sono disponibili nelle stored procedure.  
  
 Le stored procedure devono essere in un determinato ambito (il server o il database) per essere visibili nel livello MDX (Multidimensional Expressions) e quindi essere chiamate. Tuttavia, dopo che una stored procedure viene chiamata, il suo ambito non viene limitato alle azioni consentite dal relativo padre. Una stored procedure può infatti apportare cambiamenti o modifiche in qualsiasi punto del server ed è soggetta solo a limitazioni di sicurezza del processo utente che l'ha richiamata o a limitazioni alla transazione nella quale è in esecuzione.  
  
 Le procedure nell'ambito del server sono disponibili in tutti i contesti del server. Le stored procedure nell'ambito del database sono visibili solo nel contesto del database nel quale sono state definite.  
  
 Come qualsiasi altra funzione MDX, una stored procedure deve essere risolta prima che possa proseguire una sessione MDX. Le stored procedure bloccano le sessioni MDX durante l'esecuzione. A meno che non esista una ragione specifica per interrompere una sessione MDX con una interazione con l'utente in corso, è consigliabile evitare interazioni con l'utente, quali ad esempio le finestre di dialogo.  
  
## <a name="dependent-assemblies"></a>Assembly dipendenti  
 Affinché il CLR (Common Language Runtime) trovi tutti gli assembly dipendenti, questi devono essere caricati in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivia gli assembly dipendenti nella stessa cartella dell'assembly principale, pertanto CLR risolve automaticamente ogni riferimento alla funzione in tali assembly.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definizione delle stored procedure](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
