---
title: Proprietà ReadyState (RDS) | Microsoft Docs
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
ms.openlocfilehash: 8a2a3d22f30a865687e38aedfaf6e688e677efae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963587"
---
# <a name="readystate-property-rds"></a>Proprietà ReadyState (Servizi Desktop remoto)
Indica lo stato di un oggetto [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) quando recupera i dati nell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce uno dei valori seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|La query corrente è ancora in esecuzione e non è stata recuperata alcuna riga. Il **Recordset** dell'oggetto **DataControl** non è disponibile per l'utilizzo.|  
|**adcReadyStateInteractive**|Un set iniziale di righe recuperato dalla query corrente è stato archiviato nel **Recordset** dell'oggetto **DataControl** e disponibile per l'utilizzo. È ancora in corso il recupero delle righe rimanenti.|  
|**adcReadyStateComplete**|Tutte le righe recuperate dalla query corrente sono state archiviate nel **Recordset** dell'oggetto **DataControl** e sono disponibili per l'utilizzo.<br /><br /> Questo stato sarà presente anche se un'operazione è stata interrotta a causa di un errore o se l'oggetto **Recordset** non è inizializzato.|  
  
> [!NOTE]
>  Ogni file eseguibile lato client che utilizza queste costanti deve fornire le relative dichiarazioni. È possibile tagliare e incollare le dichiarazioni di costanti desiderate dal file Adcvbs. Inc, che si trova nella cartella di installazione predefinita per la libreria RDS.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare l'evento [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) per monitorare le modifiche apportate alla proprietà **ReadyState** durante un'operazione di query asincrona. Questa operazione è più efficiente rispetto al controllo periodico del valore della proprietà.  
  
 Se si verifica un errore durante un'operazione asincrona, la proprietà **ReadyState** viene modificata in **adcReadyStateComplete**, la proprietà [state](../../../ado/reference/ado-api/state-property-ado.md) passa da **AdStateExecuting** a **adStateClosed**e la proprietà del [valore](../../../ado/reference/ado-api/value-property-ado.md) dell'oggetto **Recordset** rimane *null*.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ReadyState (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Metodo Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Proprietà ExecuteOptions (Servizi Desktop remoto)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


