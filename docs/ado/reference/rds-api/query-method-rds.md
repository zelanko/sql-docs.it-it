---
title: Metodo query (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f646d5ebee63981c882f5e1ece147be0ff1677e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963820"
---
# <a name="query-method-rds"></a>Metodo Query (Servizi Desktop remoto)
Usa una stringa di query SQL valida per restituire un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Recordset*  
 Variabile oggetto che rappresenta un oggetto **Recordset** .  
  
 *DataFactory*  
 Variabile oggetto che rappresenta un oggetto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *Connessione*  
 Valore **stringa** che contiene le informazioni di connessione al server. Questa operazione è simile alla proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md) .  
  
 *Query*  
 **Stringa** che contiene la query SQL.  
  
## <a name="remarks"></a>Osservazioni  
 La query deve usare il sottolinguaggio SQL del server di database. Se si verifica un errore con la query eseguita, viene restituito lo stato del risultato. Il metodo di **query** non esegue alcun controllo della sintassi sulla stringa di **query** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di oggetto DataFactory, metodo Query e metodo CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


