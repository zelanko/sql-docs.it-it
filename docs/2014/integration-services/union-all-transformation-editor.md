---
title: Editor trasformazione Unione input multipli | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- Union All Transformation Editor
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6414b887ee88ddc0281ee86fd3236f026b8a3f28
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972641"
---
# <a name="union-all-transformation-editor"></a>Editor trasformazione Unione input multipli
  Utilizzare la finestra di dialogo **Editor trasformazione Unione input multipli** per unire diversi set di righe di input in un unico set di righe di output. Includendo la trasformazione Unione input multipli in un flusso di dati è possibile unire dati tratti da più flussi di dati, creare set di dati complessi nidificando più trasformazioni Unione input multipli e unire nuovamente le righe dopo la correzione degli errori nei dati.  
  
 Per ulteriori informazioni sulla trasformazione Unione input multipli, vedere [Union All Transformation](data-flow/transformations/union-all-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Nome colonna di output**  
 Consente di digitare un alias per ogni colonna. Per impostazione predefinita, viene suggerito il nome della colonna del primo input, ovvero l'input di riferimento. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Input unione input multipli 1**  
 Consente di selezionare nell'elenco di colonne di input disponibili nel primo input, ovvero l'input di riferimento. I metadati delle colonne mappate devono corrispondere.  
  
 **Input unione input multipli n**  
 Consente di selezionare nell'elenco di colonne di input disponibili nel secondo input e negli input aggiuntivi. I metadati delle colonne mappate devono corrispondere.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Unione di dati tramite la trasformazione Unione input multipli](data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [Trasformazione Unione](data-flow/transformations/merge-transformation.md)   
 [Trasformazione Merge join](data-flow/transformations/merge-join-transformation.md)  
  
  
