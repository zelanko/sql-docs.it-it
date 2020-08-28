---
description: Evento onError (Servizi Desktop remoto)
title: Evento OnError (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onError event [ADO]
ms.assetid: b01cbc62-fbd7-4068-b16c-8b0f80a05887
author: rothja
ms.author: jroth
ms.openlocfilehash: adef4e3eea01e966b87f939ce1a5b961ba87847b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981902"
---
# <a name="onerror-event-rds"></a>Evento onError (Servizi Desktop remoto)
L'evento **OnError** viene chiamato ogni volta che si verifica un errore durante un'operazione.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
onError SCode, Description, Source, CancelDisplay  
```  
  
#### <a name="parameters"></a>Parametri  
 *SCode*  
 Intero che indica il codice di stato dell'errore.  
  
 *Descrizione*  
 **Stringa** che indica una descrizione dell'errore.  
  
 *Origine*  
 **Stringa** che indica la query o il comando che ha causato l'errore.  
  
 *CancelDisplay*  
 Valore **booleano** che, se impostato su **true**, impedisce che l'errore venga visualizzato in una finestra di dialogo.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../guide/data/ado-event-handler-summary.md)