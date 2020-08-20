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
ms.openlocfilehash: 6427b808d31c9b1938b093da2bdf14d59bec90cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457363"
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
 [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
