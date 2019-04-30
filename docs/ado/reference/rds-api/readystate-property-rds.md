---
title: Proprietà ReadyState (Servizi Desktop remoto) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c575683b5ec23c6739a37eae177be004efea0a57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63255727"
---
# <a name="readystate-property-rds"></a>Proprietà ReadyState (Servizi Desktop remoto)
Indica lo stato di un [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto come il recupero di dati nel relativo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|La query corrente è ancora in esecuzione e non di righe recuperate. Il **DataControl** dell'oggetto **Recordset** non è disponibile per l'uso.|  
|**adcReadyStateInteractive**|Un set iniziale di righe recuperate alla query corrente è stato archiviato nel **DataControl** dell'oggetto **Recordset** e sono disponibili per l'uso. Le righe rimanenti sono ancora recuperate.|  
|**adcReadyStateComplete**|Tutte le righe recuperate alla query corrente sono state archiviate nel **DataControl** dell'oggetto **Recordset** e sono disponibili per l'uso.<br /><br /> Questo stato si verificherà anche se un'operazione interrotta a causa di un errore o se il **Recordset** oggetto non inizializzato.|  
  
> [!NOTE]
>  Ogni file eseguibile dal lato client che usa le costanti debba fornire le relative dichiarazioni. È possibile tagliare e incollare le dichiarazioni costante desiderati dal file Adcvbs. Inc, che si trova nella cartella di installazione predefinito per la libreria di servizi desktop remoto.  
  
## <a name="remarks"></a>Note  
 Usare la [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) evento per monitorare le modifiche le **ReadyState** proprietà durante un'operazione di query asincrona. Questo è più efficiente rispetto alla verifica periodicamente il valore della proprietà.  
  
 Se si verifica un errore durante un'operazione asincrona, il **ReadyState** le modifiche alle proprietà **adcReadyStateComplete**, il [stato](../../../ado/reference/ado-api/state-property-ado.md) proprietà viene cambiata da **adStateExecuting** alla **adStateClosed**e il **Recordset** oggetto [valore](../../../ado/reference/ado-api/value-property-ado.md) rimane impostato su proprietà *Nothing* .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ReadyState (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Metodo Cancel (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Proprietà ExecuteOptions (Servizi Desktop remoto)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


