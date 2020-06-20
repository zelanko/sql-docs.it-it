---
title: Processore fantasma XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 14158b7097427b6704cf5e747fa998a11217ecd6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016785"
---
# <a name="xtp-phantom-processor"></a>XTP Phantom Processor
  L'oggetto prestazione XTP Phantom Processor contiene contatori correlati al sottosistema di elaborazione fantasma del motore XTP. Con questo componente è possibile rilevare le righe fantasma nelle transazioni in esecuzione a livello di isolamento SERIALIZABLE.  
  
 Questa tabella descrive i contatori **XTP Phantom Processor** .  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|**Tentativi di analisi di elementi nascosti/sec (eseguiti dal processore fantasma)**|Numero medio di tentativi di analisi dovuti a conflitti di scrittura durante le operazioni su elementi nascosti eseguite dal processore fantasma, al secondo. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|  
|**Righe fantasma scadute rimosse/sec**|Numero medio di righe scadute rimosse dalle analisi fantasma, al secondo.|  
|**Righe fantasma scadute interessate/sec**|Numero medio di righe scadute interessate dalle analisi fantasma, al secondo.|  
|**Righe fantasma in scadenza interessate/sec**|Numero medio di righe in scadenza interessate dalle analisi fantasma, al secondo.|  
|**Righe fantasma interessate/sec**|Numero medio di righe interessate dalle analisi fantasma, al secondo.|  
|**Analisi fantasma avviate/sec**|Numero medio di analisi fantasma avviate, al secondo.|  
  
## <a name="see-also"></a>Vedere anche  
 [XTP &#40;i contatori delle prestazioni di OLTP in memoria&#41;](../../integration-services/performance/performance-counters.md)  
  
  
