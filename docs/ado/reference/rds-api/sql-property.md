---
title: Proprietà SQL | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba032adaa8b6412b9390de644504cae6c55c74f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697709"
---
# <a name="sql-property"></a>Proprietà SQL
Indica la stringa di query usata per recuperare il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 È possibile impostare il **SQL** proprietà in fase di progettazione nel [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) tag di oggetti dell'oggetto, o in fase di esecuzione nel codice di script.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parametri  
 *QueryString*  
 Oggetto **stringa** valore contenente una richiesta di dati SQL valida.  
  
 *DataControl*  
 Una variabile oggetto che rappresenta un **Servizi Desktop remoto. DataControl** oggetto.  
  
## <a name="remarks"></a>Note  
 In generale, si tratta di un'istruzione SQL, utilizzando il sottolinguaggio del server di database, ad esempio `"Select * from NewTitles"`. Per garantire che i record corrispondenti e aggiornati in modo accurato, una query aggiornabile deve contenere un campo diverso da un campo binario lungo o un campo calcolato.  
  
 Il **SQL** proprietà è facoltativa se un oggetto business sul lato server personalizzato consente di recuperare i dati per il client.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà SQL (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Proprietà Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Metodo query (Servizi Desktop remoto)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Metodo Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


