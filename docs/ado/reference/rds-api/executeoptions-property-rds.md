---
description: Proprietà ExecuteOptions (Servizi Desktop remoto)
title: Proprietà ExecuteOptions (RDS) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dacac570cac3525593f281e52742f4efeb8cba4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439033"
---
# <a name="executeoptions-property-rds"></a>Proprietà ExecuteOptions (Servizi Desktop remoto)
Indica se l'esecuzione asincrona è abilitata.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce uno dei valori seguenti.  
  
|Costante|Descrizione|  
|--------------|-----------------|  
|**adcExecSync**|Esegue in modo sincrono l'aggiornamento successivo del [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .|  
|**adcExecAsync**|Valore predefinito. Esegue l'aggiornamento successivo del **Recordset** in modo asincrono.|  
  
> [!NOTE]
>  Ogni file eseguibile che usa queste costanti deve fornire le relative dichiarazioni. È possibile tagliare e incollare le dichiarazioni di costanti desiderate dal file Adcvbs. Inc, che si trova nella cartella di installazione predefinita per la libreria RDS.  
  
## <a name="remarks"></a>Osservazioni  
 Se **ExecuteOptions** è impostato su **adcExecAsync**, viene eseguita in modo asincrono la successiva chiamata di **aggiornamento** sul Servizi Desktop remoto [. ](../../../ado/reference/rds-api/datacontrol-object-rds.md) **Recordset**dell'oggetto DataControl.  
  
 Se si tenta di chiamare [Reset](../../../ado/reference/rds-api/reset-method-rds.md), [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md), [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)o [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) mentre un'altra operazione asincrona potrebbe modificare [RDS. ](../../../ado/reference/rds-api/datacontrol-object-rds.md) Il **Recordset** dell'oggetto DataControl è in esecuzione. si verifica un errore.  
  
 Se si verifica un errore durante un'operazione asincrona, **RDS. ** Il valore [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) dell'oggetto DataControl viene modificato da **adcReadyStateLoaded** a **AdcReadyStateComplete**e il valore della proprietà **Recordset** rimane *null*.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ExecuteOptions e FetchOptions (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Metodo Cancel (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancel-method-rds.md)


