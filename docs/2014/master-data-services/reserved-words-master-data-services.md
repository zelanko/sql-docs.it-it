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
ms.openlocfilehash: cd1e5bcee01992607cf9bffca1a72dd99bd75fbe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960581"
---
# <a name="reserved-words-master-data-services"></a>Parole riservate (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], quando si creano oggetti modello o membri, alcune parole non possono essere utilizzate. È possibile che l'utilizzo di queste parole provochi errori.  
  
> [!NOTE]  
>  Inoltre, è necessario limitare l'utilizzo di caratteri speciali (simboli, sillabazione e così via).  
  
-   [Modelli](#models)  
  
-   [Entità](#entities)  
  
-   [Gerarchie esplicite](#exhierarchies)  
  
-   [Attributes (Attributi)](#attributes)  
  
-   [Membri](#members)  
  
##  <a name="models"></a><a name="models"></a>Modelli  
 Se si crea un modello con il nome impostato su **nome**, non selezionare **Crea entità con lo stesso nome del modello** perché non è possibile utilizzare il **nome** per il nome di un'entità.  
  
##  <a name="entities"></a><a name="entities"></a>Entità  
 Per i nomi dell'entità, non è possibile utilizzare **Name** o **Code**.  
  
##  <a name="explicit-hierarchies"></a><a name="exhierarchies"></a>Gerarchie esplicite  
 Per i nomi della gerarchia espliciti, non è possibile utilizzare **Name** o **Code**.  
  
##  <a name="attributes"></a><a name="attributes"></a>Attributi  
  
-   **ID**  
  
-   **Codice**  
  
-   **Nome**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a><a name="members"></a>Membri  
 Per i membri, non è possibile usare **MDMMemberStatus** o **root** per il valore dell'attributo **Code** .  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Master Data Services](master-data-services-overview-mds.md)  
  
  
