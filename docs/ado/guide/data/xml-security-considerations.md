---
title: Considerazioni sulla sicurezza XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8e5ef2215725382650540d24f90e7cbd61102a71
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704431"
---
# <a name="xml-security-considerations"></a>Considerazioni sulla sicurezza per XML
I metodi Open nell'oggetto Recordset e salvare ADO non sono considerati operazioni di sicuro per l'esecuzione in Internet Explorer. Di conseguenza, se questi metodi vengono usati in un codice di script che è in esecuzione in un'applicazione o un controllo che è ospitato in un browser, la configurazione della sicurezza del browser avrà un effetto sul relativo comportamento.  
  
 Internet Explorer 5 offre le restrizioni di sicurezza per tali operazioni per impostazione predefinita nelle aree di Internet. Con questa configurazione, il set di record non è possibile apportare qualsiasi accesso al file system locale sul client o tutte le origini dati all'esterno del dominio del server da cui è stata scaricata la pagina di accesso. In particolare, quando si esegue all'interno dell'host di browser, un set di record può essere salvato in un file solo se è nello stesso server dal quale è stata scaricata la pagina. Analogamente, è possibile aprire un set di record mediante il caricamento da un file solo se tale file è nello stesso server dal quale è stata scaricata la pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
