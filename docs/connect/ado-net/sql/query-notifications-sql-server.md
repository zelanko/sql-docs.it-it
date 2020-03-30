---
title: Notifiche di query in SQL Server
description: Viene descritto in che modo le applicazioni .NET possono richiedere una notifica da SQL Server in seguito a modifiche dei dati.
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 57222c852ac2ba8c1aedf42075b69587a4b3843d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896572"
---
# <a name="query-notifications-in-sql-server"></a>Notifiche di query in SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Basate sull'infrastruttura di Service Broker, tali notifiche consentono di comunicare alle applicazioni che i dati sono stati modificati. Questa caratteristica è particolarmente utile per le applicazioni che forniscono una cache di informazioni provenienti da un database, ad esempio un'applicazione Web, e devono essere notificate quando i dati di origine vengono modificati.  
  
Esistono tre modi per implementare le notifiche delle query tramite ADO.NET:  
  
- L'implementazione di basso livello viene offerta dalla classe `SqlNotificationRequest` che espone la funzionalità lato server, consentendo di eseguire un comando con una richiesta di notifica.  
  
- L'implementazione di alto livello viene offerta dalla classe `SqlDependency`, ovvero una classe che offre un'astrazione di alto livello della funzionalità di notifica tra l'applicazione di origine e SQL Server, consentendo di usare una dipendenza per rilevare le modifiche nel server. Nella maggior parte dei casi si tratta del modo più semplice ed efficace per sfruttare la funzionalità di notifica di SQL Server in applicazioni client gestite, usando il provider di dati Microsoft SqlClient per SQL Server.  
  
- Inoltre, nelle applicazioni Web create con ASP.NET 2.0 o versioni successive è possibile usare le classi helper `SqlCacheDependency`.  
  
Le notifiche delle query sono utili per applicazioni che richiedono l'aggiornamento delle visualizzazioni o delle cache in seguito a modifiche dei dati sottostanti. Microsoft SQL Server consente ad applicazioni .NET di inviare un comando a SQL Server e di richiedere che venga generata una notifica se l'esecuzione dello stesso produrrebbe set di risultati diversi da quelli recuperati inizialmente. Le notifiche generate nel server vengono inviate tramite code in modo da essere elaborate in un secondo momento.  
  
È possibile impostare le notifiche per le istruzioni SELECT e EXECUTE. Quando si usa un'istruzione EXECUTE, SQL Server registra una notifica del comando eseguito anziché l'istruzione EXECUTE stessa. Il comando deve soddisfare i requisiti e le limitazioni per un'istruzione SELECT. Se un comando che registra una notifica contiene più istruzioni, il motore di database crea una notifica per ogni istruzione del batch.  
  
Se si sviluppa un'applicazione in cui sono necessarie notifiche in frazioni di secondo affidabili quando i dati vengono modificati, vedere le sezioni **Pianificazione di una strategia delle notifiche delle query efficiente** e **Alternative alle notifiche delle query** nell'argomento [Pianificazione delle notifiche](https://go.microsoft.com/fwlink/?LinkId=211984) nella documentazione online di SQL Server. Per altre informazioni sulle notifiche delle query e su SQL Server Service Broker, vedere i collegamenti seguenti agli argomenti della documentazione online di SQL Server.  
  
**Documentazione di SQL Server**  
  
- [Uso delle notifiche delle query](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [Creazione di una query da notificare](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Sviluppo (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Centro informazioni per lo sviluppatore di Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guida per gli sviluppatori di Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Abilitazione di notifiche di query](enable-query-notifications.md)  
Illustra come usare le notifiche delle query, inclusi i requisiti per abilitarle e usarle.  
  
[SqlDependency in un'applicazione ASP.NET](sqldependency-aspnet-app.md)  
Illustra l'uso delle notifiche delle query da un'applicazione ASP.NET.  
  
[Rilevamento di modifiche con SqlDependency](detect-changes-sqldependency.md)  
Illustra come rilevare i casi in cui i risultati della query si differenziano da quelli ricevuti in origine.  
  
[Esecuzione di SqlCommand con SqlNotificationRequest](sqlcommand-execution-sqlnotificationrequest.md)  
Illustra la configurazione di un oggetto <xref:Microsoft.Data.SqlClient.SqlCommand> da usare con una notifica delle query.  
  
## <a name="reference"></a>Riferimento  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
Descrive la classe <xref:Microsoft.Data.Sql.SqlNotificationRequest> e tutti i relativi membri.  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
Descrive la classe <xref:Microsoft.Data.SqlClient.SqlDependency> e tutti i relativi membri.  
  
<xref:System.Web.Caching.SqlCacheDependency>  
Descrive la classe <xref:System.Web.Caching.SqlCacheDependency> e tutti i relativi membri.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
