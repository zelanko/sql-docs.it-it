---
title: Metodo SubmitChanges (Servizi Desktop remoto) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0655a76463f7a0a1507fa2767eade3cb37c48a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710196"
---
# <a name="submitchanges-method-rds"></a>Metodo SubmitChanges (Servizi Desktop remoto)
Invia le modifiche in locale memorizzata nella cache e aggiornabile in sospeso [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per l'origine dati specificata nel [Connect](../../../ado/reference/rds-api/connect-property-rds.md) proprietà o nella [URL](../../../ado/reference/rds-api/url-property-rds.md) proprietà.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *DataFactory*  
 Una variabile oggetto che rappresenta un' [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto.  
  
 *Connessione*  
 Oggetto **stringa** valore che rappresenta la connessione creata con il **Servizi Desktop remoto. DataControl** dell'oggetto [Connect](../../../ado/reference/rds-api/connect-property-rds.md) proprietà.  
  
 *Recordset*  
 Una variabile oggetto che rappresenta un **Recordset** oggetto.  
  
## <a name="remarks"></a>Note  
 Il [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), e [SQL](../../../ado/reference/rds-api/sql-property.md) devono essere impostate prima di poter usare il **SubmitChanges** metodo con il  **SERVIZI DESKTOP REMOTO. DataControl** oggetto.  
  
 Se si chiama il [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) metodo dopo aver chiamato **SubmitChanges** per lo stesso **Recordset** oggetto, il **CancelUpdate** chiamata ha esito negativo perché le modifiche sono state già eseguito il commit.  
  
 Solo i record modificati vengono inviati per la modifica e su tutte le modifiche esito positivo o negativo di tutte le modifiche tra loro.  
  
 È possibile usare **SubmitChanges** solo con il valore predefinito **RDSServer** oggetto. Oggetti business personalizzati non è possibile usare questo metodo.  
  
 Se il **URL** proprietà è stata impostata, **SubmitChanges** invierà le modifiche nel percorso specificato dall'URL.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Comando pulsanti di Address Book](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Metodo CancelUpdate (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Refresh (Servizi Desktop remoto)](../../../ado/reference/rds-api/refresh-method-rds.md)



