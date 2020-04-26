---
title: Creare e gestire misure (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6087d5fa39dd023d13ce3f49fbdfb855f12b921c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067445"
---
# <a name="create-and-manage-measures-ssas-tabular"></a>Creare e gestire misure (SSAS tabulare)
  Una misura è una formula creata per l'utilizzo in un report o in una tabella pivot o grafico pivot. Le misure possono essere basate sulle funzioni di aggregazione standard, ad esempio COUNT o SUM. In alternativa, è possibile definire formule personalizzate tramite DAX. Nelle attività di questo argomento viene descritto come creare e gestire misure utilizzando la griglia delle misure di una tabella.  
  
 In questo argomento sono incluse le attività seguenti:  
  
-   [Per creare una misura tramite una formula di aggregazione standard](#bkmk_create_stand)  
  
-   [Per creare una misura tramite una formula personalizzata](#bkmk_create_custom)  
  
-   [Per modificare le proprietà di una misura](#bkmk_edit)  
  
-   [Per rinominare una misura](#bkmk_rename)  
  
-   [Per eliminare una misura](#bkmk_delete)  
  
## <a name="tasks"></a>Attività  
 Per creare e gestire misure, sarà necessario utilizzare la griglia delle misure di una tabella. La griglia delle misure per una tabella può essere visualizzata solo in Vista dati di Progettazione modelli. Non è possibile creare misure o visualizzare la griglia delle misure in Vista diagramma; tuttavia, in tale vista è possibile visualizzare misure esistenti. Per visualizzare la griglia delle misure per una tabella, fare clic sul menu **Tabella** , quindi su **Mostra griglia delle misure**.  
  
###  <a name="to-create-a-measure-using-a-standard-aggregation-formula"></a><a name="bkmk_create_stand"></a>Per creare una misura utilizzando una formula di aggregazione standard  
  
-   Fare clic sulla colonna per la quale si desidera creare la misura, selezionare il menu **Colonna** , scegliere **Somma automatica**, quindi fare clic su un tipo di aggregazione.  
  
     La misura verrà creata automaticamente con un nome predefinito, seguito dalla formula nella prima cella nella griglia delle misure direttamente sotto la colonna.  
  
###  <a name="to-create-a-measure-using-a-custom-formula"></a><a name="bkmk_create_custom"></a> Per creare una misura tramite una formula personalizzata  
  
-   Nella griglia delle misure, sotto la colonna per la quale si desidera creare la misura, fare clic su una cella, quindi nella barra della formula digitare un nome, seguito da due punti (:), da un segno di uguale (=) e dalla formula. Premere INVIO per accettare la formula.  
  
###  <a name="to-edit-measure-properties"></a><a name="bkmk_edit"></a>Per modificare le proprietà di una misura  
  
-   Nella griglia delle misure fare clic su una misura, quindi nella finestra **Proprietà** digitare o selezionare un altro valore della proprietà.  
  
###  <a name="to-rename-a-measure"></a><a name="bkmk_rename"></a>Per rinominare una misura  
  
-   Nella griglia delle misure fare clic su una misura e, in **Nome misura** della finestra **Proprietà**digitare un nuovo nome, quindi fare clic su INVIO.  
  
     Inoltre, è possibile rinominare una misura nella barra della formula. Il nome della misura precede la formula, seguito da due punti (:).  
  
###  <a name="to-delete-a-measure"></a><a name="bkmk_delete"></a>Per eliminare una misura  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse su una misura, quindi scegliere **Elimina**.  
  
## <a name="see-also"></a>Vedi anche  
 [Misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md)   
 [Indicatori KPI &#40;&#41;tabulare SSAS](kpis-ssas-tabular.md)   
 [Colonne calcolate &#40;SSAS tabulare&#41;](ssas-calculated-columns.md)  
  
  
