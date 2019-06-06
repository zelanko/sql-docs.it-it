---
title: Evento onReadyStateChange (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5fc38ed5f4c7fb7e2d12eaa1853b57eb0cdbc13a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712560"
---
# <a name="onreadystatechange-event-rds"></a>Evento onReadyStateChange (Servizi Desktop remoto)
Il **onReadyStateChange** eventi viene chiamato ogni volta che il valore della [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) le modifiche alle proprietà.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parametri  
 Nessuna.  
  
## <a name="remarks"></a>Note  
 Il **ReadyState** proprietà riflette lo stato di avanzamento di un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto mentre recupera in modo asincrono i dati nel relativo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto. Usare la **onReadyStateChange** evento per monitorare le modifiche le **ReadyState** proprietà ogni volta che si verificano. Questo è più efficiente rispetto alla verifica periodicamente il valore della proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)


