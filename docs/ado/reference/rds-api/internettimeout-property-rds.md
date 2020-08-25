---
description: Proprietà InternetTimeout (Servizi Desktop remoto)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 83613f9083c0e532b4a2124b4beff20d4772c2fd
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768060"
---
# <a name="internettimeout-property-rds"></a>Proprietà InternetTimeout (Servizi Desktop remoto)
Indica il numero di millisecondi di attesa prima che si verifichi il timeout di una richiesta.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che rappresenta il numero di millisecondi prima del timeout di una richiesta.  
  
## <a name="remarks"></a>Commenti  
 Questa proprietà si applica solo alle richieste inviate con i protocolli HTTP o HTTPS.  
  
 Per l'esecuzione delle richieste in un ambiente a tre livelli possono essere necessari alcuni minuti. Usare questa proprietà per specificare un tempo aggiuntivo per le richieste con esecuzione prolungata.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto DataControl (Servizi Desktop remoto)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [Oggetto DataSpace (Servizi Desktop remoto)](./dataspace-object-rds.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di Proprietà InternetTimeout (VB)](./internettimeout-property-example-vb.md)   
 [Esempio della proprietà InternetTimeout (VC++)](./internettimeout-property-example-vc.md)   
