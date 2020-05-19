---
title: Considerazioni sulla sicurezza degli updategram (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a9ed4aad31f5a4697a268d82e282a135ea85c37c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717572"
---
# <a name="updategram-security-considerations-sqlxml-40"></a>Considerazioni sulla sicurezza degli updategram (SQLXML 4.0)
  Di seguito sono riportate alcune linee guida relative alla sicurezza quando si utilizzano gli updategram:  
  
-   Evitare di utilizzare il mapping predefinito quando si utilizzano gli updategram per aggiornare i dati. Quando si utilizza il mapping predefinito, il nome di un elemento di un updategram esegue il mapping al nome di una tabella e il nome di un attributo esegue il mapping a una colonna. In questo modo vengono esposte le informazioni sulle colonne e sulle tabelle di database. Ciò può costituire un potenziale rischio di sicurezza. Se invece si specifica uno schema di mapping separato che esegue il mapping degli elementi e degli attributi di un updategram alle tabelle e alle colonne di database, i nomi degli attributi e degli elementi dell'updategram possono essere arbitrari e lo schema esegue i mapping necessari di tali nomi alle tabelle e alle colonne di database. Le informazioni del database non vengono pertanto esposte in un updategram.  
  
-   Non consentire agli utenti di creare ed eseguire i relativi updategram. È consigliabile che gli updategram vengano forniti come modelli in un server anziché essere creati dinamicamente in applicazioni di tipo ASP, situazione in cui i dati del database potrebbero essere a rischio. Il potenziale rischio può essere eliminato consentendo agli utenti di accedere ai dati solo tramite gli updategram forniti come modelli.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di updategram per modificare dati in SQLXML 4.0](../updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  
