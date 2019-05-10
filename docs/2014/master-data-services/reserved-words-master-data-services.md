---
title: Parole riservate (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5435c2a48417156abd6d4f831bf61c9ba6440fab
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482569"
---
# <a name="reserved-words-master-data-services"></a>Parole riservate (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], quando si creano oggetti modello o membri, alcune parole non possono essere utilizzate. È possibile che l'utilizzo di queste parole provochi errori.  
  
> [!NOTE]  
>  Inoltre, è necessario limitare l'utilizzo di caratteri speciali (simboli, sillabazione e così via).  
  
-   [Modelli](#models)  
  
-   [Entità](#entities)  
  
-   [Gerarchie esplicite](#exhierarchies)  
  
-   [Attributi](#attributes)  
  
-   [Membri](#members)  
  
##  <a name="models"></a> Modelli  
 Se si crea un modello con il nome impostato su **Name**, non si seleziona **Crea entità con lo stesso nome del modello** perché **nome** non può essere usato per il nome di un'entità.  
  
##  <a name="entities"></a> Entità  
 Per i nomi dell'entità, non è possibile utilizzare **Name** o **Code**.  
  
##  <a name="exhierarchies"></a> Gerarchie esplicite  
 Per i nomi della gerarchia espliciti, non è possibile utilizzare **Name** o **Code**.  
  
##  <a name="attributes"></a> Attributi  
  
-   **ID**  
  
-   **Code**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Membri  
 Per i membri, non è possibile utilizzare **MDMMemberStatus** oppure **radice** per il **codice** valore dell'attributo.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Master Data Services](master-data-services-overview-mds.md)  
  
  
