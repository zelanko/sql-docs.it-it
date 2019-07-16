---
title: Proprietà ExecuteOptions (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ae55ec1fccbd491854fb8bff2daa215d38b20ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964180"
---
# <a name="executeoptions-property-rds"></a>Proprietà ExecuteOptions (Servizi Desktop remoto)
Indica se è abilitata l'esecuzione asincrona.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce uno dei valori seguenti.  
  
|Costante|Descrizione|  
|--------------|-----------------|  
|**adcExecSync**|Esegue l'aggiornamento successivo del [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in modo sincrono.|  
|**adcExecAsync**|Valore predefinito. Esegue l'aggiornamento successivo del **Recordset** in modo asincrono.|  
  
> [!NOTE]
>  Ogni file eseguibile che usa le costanti debba fornire le relative dichiarazioni. È possibile tagliare e incollare le dichiarazioni costante desiderati dal file Adcvbs. Inc, che si trova nella cartella di installazione predefinito per la libreria di servizi desktop remoto.  
  
## <a name="remarks"></a>Note  
 Se **ExecuteOptions** è impostata su **adcExecAsync**, quindi si esegue in modo asincrono alla successiva **Aggiorna** chiamare sul [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto **Recordset**.  
  
 Se si tenta di chiamare [reimpostare](../../../ado/reference/rds-api/reset-method-rds.md), [aggiornare](../../../ado/reference/rds-api/refresh-method-rds.md), [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), o [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) mentre un'altra operazione asincrona che potrebbe modificarne la [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto **Recordset** è in esecuzione, si verifica un errore.  
  
 Se si verifica un errore durante un'operazione asincrona, il **Servizi Desktop remoto. DataControl** dell'oggetto [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) valore viene modificato da **adcReadyStateLoaded** alla **adcReadyStateComplete**e il  **Recordset** valore della proprietà resta *Nothing*.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ExecuteOptions e FetchOptions (esempio di proprietà (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Metodo Cancel (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancel-method-rds.md)


