---
title: Eseguire il rollback della cronologia delle revisioni del membro
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 51465b3f3ae7193d925d30203c5a831a03b8d51a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "73727932"
---
# <a name="rollback-member-revision-history-master-data-services"></a>Rollback della cronologia delle revisioni del membro (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Una cronologia delle revisioni del membro viene registrata ogni volta che un membro viene modificato. È possibile eseguire il rollback di una cronologia delle revisioni del membro a una versione precedente.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario avere l'autorizzazione per aggiornare almeno uno degli attributi del membro selezionato. Quando si esegue il rollback di una cronologia delle revisioni, verrà eseguito il rollback di tutti i valori di attributo che possono essere aggiornati ai valori delle versioni precedenti.  
  
-   La cronologia delle revisioni è disponibile solo quando il tipo di log delle transazioni dell'entità è membro.  
  
 **Per eseguire il rollback della cronologia delle revisioni del membro**  
  
1.  In Gestione dati master, fare clic su Esplora.  
  
2.  Scegliere l'entità e il membro per eseguire il rollback.  
  
3.  Fare clic su **Visualizza cronologia**.  
  
4.  Scegliere la revisione di cui eseguire il rollback e quindi fare clic su **Rollback**.  
  
## <a name="see-also"></a>Vedere anche  
 [Cronologia revisioni membri &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Modificare il tipo di log delle transazioni dell'entità &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
