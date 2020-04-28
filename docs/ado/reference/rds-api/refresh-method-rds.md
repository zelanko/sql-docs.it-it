---
title: Metodo Refresh (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb7cb94edab6b5422c315b71c2900662f85aa1e2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963505"
---
# <a name="refresh-method-rds"></a>Metodo Refresh (Servizi Desktop remoto)
Esegue una query sull'origine dati specificata nella proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md) e aggiorna i risultati della query.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto [. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Osservazioni  
 È necessario impostare le proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md)e [SQL](../../../ado/reference/rds-api/sql-property.md) prima di utilizzare il metodo **Refresh** . Tutti i controlli associati a dati nel form associato a un Servizi Desktop remoto **. L'oggetto DataControl** rifletterà il nuovo set di record. Qualsiasi oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) preesistente viene rilasciato e tutte le modifiche non salvate vengono ignorate. Il metodo **Refresh** rende automaticamente il primo record il record corrente.  
  
 È consigliabile chiamare periodicamente il metodo **Refresh** quando si utilizzano i dati. Se si recuperano dati e quindi lo si lascia in un computer client per un periodo di tempo, è probabile che diventi obsoleto. È possibile che le modifiche apportate non vengano eseguite correttamente, perché qualcun altro potrebbe aver modificato il record e inviato le modifiche prima dell'utente.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Esempio di metodo Refresh (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Pulsanti di comando Rubrica](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Metodo CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


