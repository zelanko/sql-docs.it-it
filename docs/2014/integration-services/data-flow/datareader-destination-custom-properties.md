---
title: Proprietà personalizzate della destinazione DataReader | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 62b6f628614d533e1bebcce071ce4761e73e08f7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432198"
---
# <a name="datareader-destination-custom-properties"></a>Proprietà personalizzate della destinazione DataReader
  La destinazione DataReader include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione DataReader. Tutte le proprietà, ad eccezione di `DataReader`, sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|DataReader|string|Nome di classe della destinazione DataReader.|  
|FailOnTimeout|Boolean|Indica se generare un errore quando si verifica un `ReadTimeout`. Il valore predefinito di questa proprietà è **False**.|  
|ReadTimeout|Integer|Numero di millisecondi prima di un timeout. Il valore predefinito di questa proprietà è 30000 (30 secondi).|  
  
 L'input e le colonne di input della destinazione DataReader non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione DataReader](datareader-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
