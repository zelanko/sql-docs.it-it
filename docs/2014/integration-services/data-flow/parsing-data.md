---
title: Analisi dei dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd52b851d4ff35fe1fc9a3a9fed05be0b8098fa9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900990"
---
# <a name="parsing-data"></a>Analisi dei dati
  I flussi di dati nei pacchetti consentono di estrarre e caricare dati da archivi dati eterogenei, in cui possono venire utilizzati numerosi diversi tipi di dati standard e personalizzati. In un flusso di dati le origini di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono responsabili dell'estrazione dei dati, dell'analisi dei dati stringa e della conversione dei dati in un tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Le trasformazioni successive possono analizzare dati per convertirli in un tipo di dati diverso oppure creare copie delle colonne con tipi di dati diversi. Anche le espressioni utilizzate nei componenti possono eseguire il cast di argomenti e operandi a tipi di dati diversi. Quando infine i dati vengono caricati in un archivio dati, la destinazione può analizzare i dati per convertirli in un tipo di dati utilizzato dalla destinazione. Per altre informazioni, vedere [Tipi di dati di Integration Services](integration-services-data-types.md).  
  
## <a name="types-of-parsing"></a>Tipi di analisi  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre due tipi di analisi per la conversione dei dati: l'analisi veloce e l'analisi standard.  
  
-   L'analisi veloce è un semplice set di routine di analisi veloci, che non supportano conversioni di tipi di dati specifiche delle impostazioni locali e supportano solo i formati di data e ora utilizzati più di frequente. Per altre informazioni, vedere [Analisi veloce](../fast-parse.md).  
  
-   L'analisi standard è un set completo di routine di analisi che supportano tutte le conversioni dei tipi di dati offerte dalle API per la conversione dei tipi di dati di automazione disponibili in Oleaut32.dll e Ole2dsip.dll. Per altre informazioni, vedere [Analisi standard](../standard-parse.md).  
  
  
