---
title: Metodo SubmitChanges (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 3291b5ca72ab984ecd8487612384ece6d5b76f9a
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942278"
---
# <a name="submitchanges-method-rds"></a>Metodo SubmitChanges (Servizi Desktop remoto)
Invia le modifiche in sospeso del [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) memorizzato nella cache locale e aggiornabile all'origine dati specificata nella proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md) o nella proprietà [URL](../../../ado/reference/rds-api/url-property-rds.md) .  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto [. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *DataFactory*  
 Variabile oggetto che rappresenta un oggetto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *Connessione*  
 Valore **stringa** che rappresenta la connessione creata con **RDS. **Proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md) dell'oggetto DataControl.  
  
 *Recordset*  
 Variabile oggetto che rappresenta un oggetto **Recordset** .  
  
## <a name="remarks"></a>Osservazioni  
 Per poter usare il metodo **SubmitChanges** con RDS, è necessario impostare le proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md)e [SQL](../../../ado/reference/rds-api/sql-property.md) **. Oggetto DataControl** .  
  
 Se si chiama il metodo [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) dopo aver chiamato **SubmitChanges** per lo stesso oggetto **Recordset** , la chiamata a **CancelUpdate** ha esito negativo perché è già stato eseguito il commit delle modifiche.  
  
 Solo i record modificati vengono inviati per la modifica e tutte le modifiche vengono riuscite o tutte le modifiche vengono interrotte insieme.  
  
 È possibile usare **SubmitChanges** solo con l'oggetto **RDSServer. DataFactory** predefinito. Gli oggetti business personalizzati non possono utilizzare questo metodo.  
  
 Se è stata impostata la proprietà **URL** , **SubmitChanges** invierà le modifiche al percorso specificato dall'URL.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Pulsanti di comando Rubrica](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Metodo CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Refresh (Servizi Desktop remoto)](../../../ado/reference/rds-api/refresh-method-rds.md)



