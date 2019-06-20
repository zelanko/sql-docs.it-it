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
manager: jroth
ms.openlocfilehash: 9992b0f7e7281ec318f978ff487107fc832c961f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697529"
---
# <a name="refresh-method-rds"></a>Metodo Refresh (Servizi Desktop remoto)
Riesegue l'origine dati specificata una query di [Connect](../../../ado/reference/rds-api/connect-property-rds.md) proprietà e gli aggiornamenti, i risultati della query.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
## <a name="remarks"></a>Note  
 È necessario impostare il [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), e [SQL](../../../ado/reference/rds-api/sql-property.md) proprietà prima di usare il **Aggiorna** (metodo). Tutti i controlli con associazione a dati nel form di cui è associato un **Servizi Desktop remoto. DataControl** oggetto rifletterà il nuovo set di record. Eventualmente preesistenti [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto viene rilasciato e non vengono eliminate eventuali modifiche non salvate. Il **Aggiorna** metodo effettua automaticamente il primo record del record corrente.  
  
 È consigliabile chiamare il **Aggiorna** metodo periodicamente quando si utilizzano i dati. Se si recuperano dati e quindi lasciarlo in un computer client per un periodo di tempo, è probabile che diventano obsolete. È possibile che eventuali modifiche apportate non riuscirà, perché un altro utente potrebbe avere modificato il record ed è stato inviato prima di procedere.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Esempio del metodo Refresh (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Comando pulsanti di Address Book](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Metodo CancelUpdate (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


