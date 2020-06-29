---
title: Editor trasformazione Merge join | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b74b8cd3e010f372cf0c0a50f5c0e19054924d0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424598"
---
# <a name="merge-join-transformation-editor"></a>Editor trasformazione Merge join
  Utilizzare la finestra di dialogo **Editor trasformazione Merge join** per specificare il tipo di join, le colonne di join e le colonne di output per l'unione di due input combinati tramite un join.  
  
> [!IMPORTANT]  
>  Per eseguire la trasformazione Merge join, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Per ulteriori informazioni sulla trasformazione Merge Join, vedere [Merge Join Transformation](data-flow/transformations/merge-join-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Tipo di join**  
 Consente di specificare se utilizzare un inner join, un outer join sinistro o un full join.  
  
 **Inverti ordine input**  
 Il pulsante **Inverti ordine input** consente di invertire l'ordine degli input. Questa selezione può risultare utile in caso si scelga di utilizzare un outer join sinistro.  
  
 **Input**  
 Per ogni colonna che si desidera includere nell'output unito, è innanzitutto necessario procedere a una selezione nell'elenco degli input disponibili.  
  
 Gli input vengono visualizzati in due tabelle separate. Selezionare le colonne da includere nell'output. Trascinare le colonne per creare un join tra le tabelle. Per eliminare un join, selezionarlo e quindi premere CANC.  
  
 **Colonna di input**  
 Selezionare una colonna da includere nell'output unito dall'elenco delle colonne disponibili nell'input selezionato.  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Ordinare i dati per le trasformazioni Unione e merge join](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [Estendere un set di dati tramite la trasformazione Merge join](data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [Trasformazione Unione](data-flow/transformations/merge-transformation.md)   
 [Trasformazione Unione input multipli](data-flow/transformations/union-all-transformation.md)  
  
  
