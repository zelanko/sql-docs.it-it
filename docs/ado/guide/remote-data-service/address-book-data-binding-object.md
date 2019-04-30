---
title: Oggetto di associazione dati manuale di indirizzi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da63965c867c56572956ca5400a4b9dcc1281abf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214836"
---
# <a name="address-book-data-binding-object"></a>Oggetto di data binding di Address Book
L'applicazione Address Book utilizza il [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto a cui associare i dati dal database di SQL Server a un oggetto visivo (in questo caso, una tabella DHTML) nella pagina dell'applicazione client HTML. La logica di programma VBScript guidato dagli eventi Usa le [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) per:  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Eseguire query sul database, inviare gli aggiornamenti al database e aggiornare la griglia dei dati.  
  
-   Consentire agli utenti di spostarsi al primo, successivamente, precedente, o l'ultimo record nella griglia dei dati.  
  
 Il codice seguente definisce il **Servizi Desktop remoto. DataControl** componente:  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 Definisce il tag OBJECT di **Servizi Desktop remoto. DataControl** componente nel programma. Il tag include due tipi di parametri:  
  
-   Quelle associate al tag di oggetti generico.  
  
-   Quelle specifiche per il **Servizi Desktop remoto. DataControl** oggetto.  
  
## <a name="generic-object-tag-parameters"></a>Parametri del Tag OBJECT generica  
 Nella tabella seguente vengono descritti i parametri associati con il tag OBJECT.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|***CLASSID***|Numero univoco a 128 bit che identifica il tipo di oggetto incorporato nel sistema. Questo identificatore viene mantenuto nel Registro di sistema del computer locale. (Per gli ID di classe del **Servizi Desktop remoto. DataControl** oggetti, vedere [Servizi Desktop remoto. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Definisce un identificatore a livello di documento per l'oggetto incorporato che consente di identificare l'oggetto nel codice.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>SERVIZI DESKTOP REMOTO. Parametri DataControl Tag  
 Nella tabella seguente vengono descritti i parametri specifici per il **Servizi Desktop remoto. DataControl** oggetto. (Per un elenco completo del **Servizi Desktop remoto. DataControl** dell'oggetto parametri e quando relativa implementazione, vedere [Servizi Desktop remoto. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|Se si Usa HTTP, il valore è il nome del computer del server preceduto da `https://`.|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|Fornisce le informazioni di connessione necessarie per il **Servizi Desktop remoto. DataControl** per connettersi a SQL Server.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|Imposta o restituisce la stringa di query usata per recuperare il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Pulsanti di comando di Address Book](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


