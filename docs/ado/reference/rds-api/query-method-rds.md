---
title: Metodo (RDS) di query | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a64a4f1a51d678e70516f277c08071f5884492c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225839"
---
# <a name="query-method-rds"></a>Metodo Query (Servizi Desktop remoto)
Viene utilizzata una stringa di query SQL valida per restituire un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Recordset*  
 Una variabile oggetto che rappresenta un **Recordset** oggetto.  
  
 *DataFactory*  
 Una variabile oggetto che rappresenta un' [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto.  
  
 *Connessione*  
 Oggetto **stringa** valore contenente le informazioni di connessione del server. Come avviene per i [Connect](../../../ado/reference/rds-api/connect-property-rds.md) proprietà.  
  
 *Query*  
 Oggetto **stringa** che contiene la query SQL.  
  
## <a name="remarks"></a>Note  
 La query deve usare il sottolinguaggio SQL del server di database. Se si verifica un errore con la query che è stata eseguita, viene restituito uno stato di risultato. Il **Query** metodo non esegue alcun controllo su sintassi il **Query** stringa.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di oggetto DataFactory, metodo Query e metodo CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


