---
title: Dettagli dell'associazione di query (finestra di dialogo origine partizione) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionfilterexpression.f1
ms.assetid: 697874d4-3f7a-4126-96f5-37cc8e2ee306
author: minewiskan
ms.author: owend
ms.openlocfilehash: 59d2ae1fed9d22366786e21a287a621f08418a5d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539753"
---
# <a name="query-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>Dettagli dell'associazione di query (finestra di dialogo Origine partizione) (Analysis Services - Dati multidimensionali)
  Usare l'opzione **Associazione di query** della finestra di dialogo **Origine partizione** per specificare la query che restituisce i dati per la partizione. Per visualizzare questo riquadro è possibile selezionare **Associazione di query** nell'opzione **Tipo di associazione** della finestra di dialogo **Origine partizione** .  
  
## <a name="options"></a>Opzioni  
 **Origine dati**  
 Consente di selezionare l'origine dei dati su cui viene eseguita la query per fornire i dati di fatto per la partizione.  
  
 **Query**  
 Consente di digitare o modificare l'istruzione SQL utilizzata per recuperare i dati dei fatti relativi al momento in cui è stata elaborata la partizione.  
  
> [!IMPORTANT]  
>  è possibile specificare una clausola WHERE per utilizzare un subset di record per questa partizione. Quando più partizioni si basano su un'unica tabella dei fatti è essenziale evitare la duplicazione di dati. Per altre informazioni, vedere [Partition Source Dialog Box &#40;Analysis Services - Multidimensional Data&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Controllo**  
 Fare clic per verificare che l'istruzione contenuta in **Query** sia un'istruzione SQL valida.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo origine partizione &#40;Analysis Services-Dati multidimensionali&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
