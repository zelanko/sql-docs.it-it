---
title: Proprietà InternetTimeout (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eaaa72c302c9218810ce653ea59fe5ff29a54ef0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963873"
---
# <a name="internettimeout-property-rds"></a>Proprietà InternetTimeout (Servizi Desktop remoto)
Indica il numero di millisecondi di attesa prima che si verifichi il timeout di una richiesta.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che rappresenta il numero di millisecondi prima del timeout di una richiesta.  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà si applica solo alle richieste inviate con i protocolli HTTP o HTTPS.  
  
 Per l'esecuzione delle richieste in un ambiente a tre livelli possono essere necessari alcuni minuti. Usare questa proprietà per specificare un tempo aggiuntivo per le richieste con esecuzione prolungata.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Oggetto DataSpace (Servizi Desktop remoto)](../../../ado/reference/rds-api/dataspace-object-rds.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Proprietà InternetTimeout (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [Esempio di proprietà InternetTimeout (VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

