---
title: Proprietà personalizzate della destinazione DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eb252810f2136cfd478bf7ce02690d1ba84dc8d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049367"
---
# <a name="datareader-destination-custom-properties"></a>Proprietà personalizzate della destinazione DataReader

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione DataReader include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione DataReader. Tutte le proprietà, ad eccezione di **DataReader** , sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|DataReader|String|Nome di classe della destinazione DataReader.|  
|FailOnTimeout|Boolean|Indica se generare un errore quando si verifica un **ReadTimeout** . Il valore predefinito di questa proprietà è **False**.|  
|ReadTimeout|Valore intero|Numero di millisecondi prima di un timeout. Il valore predefinito di questa proprietà è 30000 (30 secondi).|  
  
 L'input e le colonne di input della destinazione DataReader non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione DataReader](../../integration-services/data-flow/datareader-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
