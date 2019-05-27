---
title: Modificare il valore di timeout per la query di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 640d07115e2a071bb5d57e87955c11670f4c38b0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085886"
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>Modificare il valore di timeout per le query di data mining
  Quando si compila un grafico di accuratezza o si esegue una query di stima, talvolta la generazione di tutti i dati necessari per la stima può richiedere una notevole quantità di tempo. Per impedire il timeout della query, è possibile modificare il valore che controlla l'intervallo di tempo durante il quale il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attende il completamento di una query.  
  
 Il valore predefinito è 15; tuttavia, se i modelli sono complessi o l'origine dati è di grandi dimensioni, questo tempo potrebbe non essere sufficiente. Se necessario, è possibile aumentare notevolmente il valore in modo da assegnare una quantità di tempo sufficiente per l'elaborazione. Se ad esempio l'opzione **Timeout query** viene impostata su 600, l'esecuzione della query può continuare per un totale di 10 minuti.  
  
 Per altre informazioni sulle query di stima, vedere [Attività e procedure relative alle query di data mining](data-mining-query-tasks-and-how-tos.md).  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>Configurare il valore di timeout per le query di data mining  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]scegliere **Opzioni** dal menu **Strumenti**.  
  
2.  Nel riquadro **Opzioni** espandere **Finestre di progettazione Business Intelligence**.  
  
3.  Fare clic sulla casella di testo **Timeout query** e digitare un valore per il numero di secondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative alle query di data mining](data-mining-query-tasks-and-how-tos.md)   
 [Query di data mining](data-mining-queries.md)  
  
  
