---
description: Oggetto di data binding di Address Book
title: Oggetto di associazione dati di Address Book | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: rothja
ms.author: jroth
ms.openlocfilehash: d6b6bb99ea218268a7ccb988acb2f49fb4898f32
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978442"
---
# <a name="address-book-data-binding-object"></a>Oggetto di data binding di Address Book
L'applicazione Rubrica usa il Servizi Desktop remoto [. Oggetto DataControl](../../reference/rds-api/datacontrol-object-rds.md) per associare i dati dal database SQL Server a un oggetto visivo, in questo caso una tabella DHTML, nella pagina HTML del client dell'applicazione. La logica del programma VBScript basata sugli eventi utilizza [RDS. DataControl](../../reference/rds-api/datacontrol-object-rds.md) per:  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Eseguire una query sul database, inviare gli aggiornamenti al database e aggiornare la griglia dei dati.  
  
-   Consente agli utenti di passare al record primo, successivo, precedente o ultimo nella griglia dei dati.  
  
 Il codice seguente definisce il Servizi Desktop remoto **. Componente DataControl** :  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 Il tag OBJECT definisce il Servizi Desktop remoto **. Componente DataControl** nel programma. Il tag include due tipi di parametri:  
  
-   Oggetti associati al tag dell'oggetto generico.  
  
-   Quelli specifici del Servizi Desktop remoto **. Oggetto DataControl** .  
  
## <a name="generic-object-tag-parameters"></a>Parametri dei tag oggetto generici  
 Nella tabella seguente vengono descritti i parametri associati al tag OBJECT.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|***CLASSID***|Numero univoco a 128 bit che identifica il tipo di oggetto incorporato nel sistema. Questo identificatore viene mantenuto nel registro di sistema del computer locale. (Per gli ID di classe di Servizi Desktop remoto **. Oggetto DataControl** , vedere [RDS. Oggetto DataControl](../../reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Definisce un identificatore a livello di documento per l'oggetto incorporato usato per identificarlo nel codice.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. Parametri dei tag DataControl  
 Nella tabella seguente vengono descritti i parametri specifici di Servizi Desktop remoto **. Oggetto DataControl** . (Per un elenco completo di Servizi Desktop remoto **. ** Parametri dell'oggetto DataControl e quando implementarli, vedere [RDS. Oggetto DataControl](../../reference/rds-api/datacontrol-object-rds.md).)  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|[SERVER](../../reference/rds-api/server-property-rds.md)|Se si usa HTTP, il valore è il nome del computer server preceduto da `https://` .|  
|[CONNECT](../../reference/rds-api/connect-property-rds.md)|Fornisce le informazioni di connessione necessarie per **RDS. DataControl** per connettersi a SQL Server.|  
|[SQL](../../reference/rds-api/sql-property.md)|Imposta o restituisce la stringa di query utilizzata per recuperare il [Recordset](../../reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Pulsanti di comando di Address Book](./address-book-command-buttons.md)