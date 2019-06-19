---
title: Esempio di proprietà InternetTimeout (Servizi Desktop remoto) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 6a5886ae206f3b16f30da406a8ccc42cc8cba7a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712460"
---
# <a name="internettimeout-property-rds"></a>Proprietà InternetTimeout (Servizi Desktop remoto)
Indica il numero di millisecondi di attesa prima del timeout di una richiesta.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che rappresenta il numero di millisecondi prima che una richiesta di verifica il timeout.  
  
## <a name="remarks"></a>Note  
 Questa proprietà si applica solo alle richieste inviate con i protocolli HTTP o HTTPS.  
  
 Le richieste in un ambiente a tre livelli possono richiedere alcuni minuti per l'esecuzione. Utilizzare questa proprietà per specificare un tempo aggiuntivo per le richieste a esecuzione prolungata.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Oggetto DataSpace (Servizi Desktop remoto)](../../../ado/reference/rds-api/dataspace-object-rds.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà InternetTimeout (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [Esempio di proprietà InternetTimeout (VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

