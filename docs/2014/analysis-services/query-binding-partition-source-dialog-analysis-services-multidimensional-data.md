---
title: Query (finestra di dialogo origine partizione) dettagli dell'associazione (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionfilterexpression.f1
ms.assetid: 697874d4-3f7a-4126-96f5-37cc8e2ee306
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c26ceea2f6dd8ad136d505269f028f47e0b9b7fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748393"
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
  
 **Controlla**  
 Fare clic per verificare che l'istruzione contenuta in **Query** sia un'istruzione SQL valida.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo origine partizione &#40;Analysis Services - dati multidimensionali&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
