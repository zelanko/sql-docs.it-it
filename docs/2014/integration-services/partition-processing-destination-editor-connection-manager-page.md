---
title: Editor destinazione elaborazione partizione (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b86348e6e7fa8331697c4a0aa3b23a494ae54a5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374759"
---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>Editor destinazione elaborazione partizione (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione elaborazione partizione** per specificare una connessione a un progetto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per ulteriori informazioni sulla destinazione elaborazione partizione, vedere [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Le attività qui descritte non si applicano ai modelli tabulari di Analysis Services.  Non è possibile eseguire il mapping di colonne di input a colonne di partizione per i modelli tabulari. È possibile utilizzare invece l'attività Esegui DDL Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) per elaborare la partizione.  
  
## <a name="options"></a>Opzioni  
 **Connection manager**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una connessione usando la finestra di dialogo **Aggiungi gestione connessione Analysis Services** .  
  
 **Elenco delle partizioni disponibili**  
 Consente di selezionare la partizione da elaborare.  
  
 **Metodo di elaborazione**  
 Consente di selezionare il metodo di elaborazione. Il valore predefinito di questa opzione è **Completo**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Aggiunta (incrementale)|Consente di eseguire un'elaborazione incrementale della partizione.|  
|Full|Consente di eseguire l'elaborazione completa della partizione.|  
|Solo dati|Consente di eseguire un'elaborazione di aggiornamento della partizione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione elaborazione partizione &#40;pagina Mapping&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)   
 [Editor destinazione elaborazione partizione &#40;pagina Avanzate&#41;](../../2014/integration-services/partition-processing-destination-editor-advanced-page.md)  
  
  
