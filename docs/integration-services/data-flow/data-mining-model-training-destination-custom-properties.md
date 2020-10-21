---
description: Proprietà personalizzate della destinazione Training modello di data mining
title: Proprietà personalizzate della destinazione Training modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ed5f1b09cbbaa4d20c891a03d9846949eedc8bc
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196444"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Proprietà personalizzate della destinazione Training modello di data mining

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La destinazione Training modello di data mining include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione Training modello di data mining. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ASConnectionId|string|Identificatore univoco della gestione connessione.|  
|ASConnectionString|string|Stringa di connessione a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|string|Tag XML che identifica la struttura di data mining utilizzata dalla trasformazione.|  
  
 L'input e le colonne di input della destinazione Training modelli di data mining non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione Training modello di data mining](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](./set-the-properties-of-a-data-flow-component.md)  
  
