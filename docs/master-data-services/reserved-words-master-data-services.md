---
title: Parole riservate
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 817e15d2fe7e91f63628826f58d6a86dd4edbcb3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727913"
---
# <a name="reserved-words-master-data-services"></a>Parole riservate (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], quando si creano oggetti modello o membri, alcune parole non possono essere utilizzate. È possibile che l'utilizzo di queste parole provochi errori.  
  
> [!NOTE]  
>  Inoltre, è necessario limitare l'utilizzo di caratteri speciali (simboli, sillabazione e così via).  
  
-   [Modelli](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [Entità](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [Gerarchie esplicite](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [Attributi](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [Membri](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> Modelli  
 Se si crea un modello con il nome impostato su **Name** o **Code**, non selezionare **Crea entità con lo stesso nome del modello** poiché non è possibile usare **Name** o **Code** per il nome di un'entità.  
  
##  <a name="entities"></a> Entità  
 Per i nomi dell'entità, non è possibile utilizzare **Name** o **Code**.  
  
##  <a name="exhierarchies"></a> Gerarchie esplicite  
 Per i nomi della gerarchia espliciti, non è possibile utilizzare **Name** o **Code**.  
  
##  <a name="attributes"></a> Attributi  
  
-   **ID**  
  
-   **Codice**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **Nome**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Membri  
 Per i membri, non è possibile usare **MDMMemberStatus**, **MDMUnused**o **ROOT** per il valore di attributo **Code** .  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md)  
  
  
