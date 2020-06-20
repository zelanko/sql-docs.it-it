---
title: Editor destinazione elaborazione partizione (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bb2efbff93fb7cc831038a7e26fe4ada44d81325
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964751"
---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>Editor destinazione elaborazione partizione (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione elaborazione partizione** per specificare una connessione a un progetto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per ulteriori informazioni sulla destinazione elaborazione partizione, vedere [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Le attività qui descritte non si applicano ai modelli tabulari di Analysis Services.  Non è possibile eseguire il mapping di colonne di input a colonne di partizione per i modelli tabulari. È possibile utilizzare invece l'attività Esegui DDL Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) per elaborare la partizione.  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuovo**  
 Consente di creare una connessione usando la finestra di dialogo **Aggiungi gestione connessione Analysis Services** .  
  
 **Elenco delle partizioni disponibili**  
 Consente di selezionare la partizione da elaborare.  
  
 **Metodo di elaborazione**  
 Consente di selezionare il metodo di elaborazione. Il valore predefinito di questa opzione è **Completo**.  
  
|valore|Description|  
|-----------|-----------------|  
|Aggiunta (incrementale)|Consente di eseguire un'elaborazione incrementale della partizione.|  
|Full|Consente di eseguire l'elaborazione completa della partizione.|  
|Solo dati|Consente di eseguire un'elaborazione di aggiornamento della partizione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione elaborazione partizione &#40;pagina mapping&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)   
 [Editor destinazione elaborazione partizione &#40;pagina Avanzate&#41;](../../2014/integration-services/partition-processing-destination-editor-advanced-page.md)  
  
  
