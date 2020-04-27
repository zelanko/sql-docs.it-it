---
title: Finestra di dialogo Unisci partizione (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26751f2cc00330716f160c115d0e839cc6d9527a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077832"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Unisci partizione (Analysis Services - Dati multidimensionali)
  Utilizzare la finestra di dialogo **Unisci partizione** in **SQL Server Management Studio** per unire le partizioni relative a un gruppo di misure in un cubo. Per visualizzare la finestra di dialogo **Unisci partizione** , è possibile fare clic con il pulsante destro del mouse sulla cartella Partizioni o su una partizione in **Esplora oggetti** e quindi scegliere **Unisci partizioni** dal menu di scelta rapida.  
  
## <a name="options"></a>Opzioni  
 **Server**  
 Consente di selezionare il nome dell'istanza di Analysis Services contenente la partizione di destinazione.  
  
 **Nome**  
 Consente di selezionare il nome di una partizione esistente da utilizzare come partizione di destinazione.  
  
 **Cartella**  
 Visualizza il nome della cartella contenente la partizione di destinazione se la partizione selezionata in Nome non utilizza la cartella predefinita relativa all'istanza di Analysis Services.  
  
 **Partizioni di origine**  
 Consente di visualizzare una griglia contenente le partizioni di origine che è possibile unire alla partizione di destinazione.  
  
> [!NOTE]  
>  È possibile unire solo le partizioni incluse nello stesso gruppo di misure che condividono la medesima struttura di aggregazione.  
  
 La griglia include le colonne seguenti:  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|**Merge**|Consente di unire la partizione di origine alla partizione di destinazione.|  
|**Nome partizione**|Visualizza il nome della partizione di origine.|  
|**Ultima elaborazione**|Visualizza la data e l'ora dell'ultima elaborazione della partizione di origine.|  
  
## <a name="see-also"></a>Vedi anche  
 [Partizioni &#40;Analysis Services Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Unire partizioni in Analysis Services &#40;SSAS - Multidimensionale&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
