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
ms.openlocfilehash: fa0e9e2df1e8ba3f44b10e662d25e536ac7962f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923351"
---
# <a name="xml-security-considerations"></a>Considerazioni sulla sicurezza per XML
I metodi ADO Save e Open sull'oggetto recordset non sono considerati operazioni sicure per l'esecuzione in Internet Explorer. Pertanto, se questi metodi vengono utilizzati in un codice di script in esecuzione in un'applicazione o in un controllo ospitato in un browser, la configurazione di sicurezza del browser avrà effetto sul comportamento.  
  
 Internet Explorer 5 fornisce restrizioni di sicurezza per le operazioni di questo tipo per impostazione predefinita nelle zone Internet. Con tale configurazione, il recordset non può accedere al file system locale sul client o accedere a tutte le origini dati esterne al dominio del server da cui è stata scaricata la pagina. In particolare, quando viene eseguito all'interno dell'host del browser, un recordset può essere salvato di nuovo in un file solo se si trova nello stesso server da cui è stata scaricata la pagina. Analogamente, è possibile aprire un recordset eseguendone il caricamento da un file solo se tale file si trova nello stesso server da cui è stata scaricata la pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
