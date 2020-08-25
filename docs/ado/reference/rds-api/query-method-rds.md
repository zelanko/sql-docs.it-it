---
description: Metodo Query (Servizi Desktop remoto)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 39bd8ccc67b0181088c267a60d6af2bf99035c02
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767930"
---
# <a name="query-method-rds"></a>Metodo Query (Servizi Desktop remoto)
Usa una stringa di query SQL valida per restituire un [Recordset](../ado-api/recordset-object-ado.md).  
  
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
 Variabile oggetto che rappresenta un oggetto [RDSServer. DataFactory](./datafactory-object-rdsserver.md) .  
  
 *Connection*  
 Valore **stringa** che contiene le informazioni di connessione al server. Questa operazione è simile alla proprietà [Connect](./connect-property-rds.md) .  
  
 *Query*  
 **Stringa** che contiene la query SQL.  
  
## <a name="remarks"></a>Commenti  
 La query deve usare il sottolinguaggio SQL del server di database. Se si verifica un errore con la query eseguita, viene restituito lo stato del risultato. Il metodo di **query** non esegue alcun controllo della sintassi sulla stringa di **query** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio dell'oggetto DataFactory e dei metodi Query e CreateObject (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)