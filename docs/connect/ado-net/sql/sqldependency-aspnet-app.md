---
title: SqlDependency in un'applicazione ASP.NET
description: Viene illustrato come usare le notifiche di query da un'applicazione ASP.NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2115d087d837118b99ee3ffded9cae0003b6d4e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451966"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency in un'applicazione ASP.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Nell'esempio riportato in questa sezione viene illustrato come utilizzare <xref:Microsoft.Data.SqlClient.SqlDependency> indirettamente sfruttando l'oggetto ASP.NET <xref:System.Web.Caching.SqlCacheDependency>. L'oggetto <xref:System.Web.Caching.SqlCacheDependency> usa un <xref:Microsoft.Data.SqlClient.SqlDependency> per ascoltare le notifiche e aggiornare correttamente la cache.  
  
> [!NOTE]
>  Il codice di esempio presuppone che siano state abilitate le notifiche delle query eseguendo gli script in [Abilitazione delle notifiche delle query](enable-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Informazioni sull'applicazione di esempio  
Nell'applicazione di esempio viene usata una singola pagina Web ASP.NET per visualizzare in un controllo <xref:System.Web.UI.WebControls.GridView> le informazioni sui prodotti disponibili nel database **AdventureWorks** di SQL Server. Quando la pagina viene caricata, il codice scrive l'ora corrente in un controllo <xref:System.Web.UI.WebControls.Label>. Definisce quindi un oggetto <xref:System.Web.Caching.SqlCacheDependency> e imposta le proprietà nell'oggetto <xref:System.Web.Caching.Cache> per archiviare i dati della cache per un massimo di tre minuti. Il codice si connette quindi al database e recupera i dati. Quando la pagina viene caricata e l'applicazione esegue ASP.NET recupererà i dati dalla cache, che è possibile verificare osservando che l'ora della pagina non cambia. Se i dati da monitorare cambiano, ASP.NET invalida la cache e ripopolano il controllo `GridView` con dati aggiornati, aggiornando l'ora visualizzata nel controllo `Label`.  
  
## <a name="creating-the-sample-application"></a>Creazione dell'applicazione di esempio  
Per creare ed eseguire l'applicazione di esempio, attenersi alla procedura seguente:  
  
1. Creare un nuovo sito Web ASP.NET.  
  
2. Aggiungere un <xref:System.Web.UI.WebControls.Label> e un controllo <xref:System.Web.UI.WebControls.GridView> alla pagina default. aspx.  
  
3. Aprire il modulo di classe della pagina e aggiungere le direttive seguenti:  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Aggiungere il codice seguente nell'evento `Page_Load` della pagina:  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. Aggiungere due metodi helper, `GetConnectionString` e `GetSQL`. La stringa di connessione definita usa la sicurezza integrata. Sarà necessario verificare che l'account in uso disponga delle autorizzazioni del database richieste e che siano abilitate le notifiche nel database di esempio **AdventureWorks**.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>Test dell'applicazione  
L'applicazione memorizza nella cache i dati visualizzati nel Web Form e li aggiorna ogni tre minuti se non è presente alcuna attività. Se viene apportata una modifica al database, la cache viene aggiornata immediatamente. Eseguire l'applicazione da Visual Studio, che carica la pagina nel browser. Il tempo di aggiornamento della cache visualizzato indica la data dell'ultimo aggiornamento della cache. Attendere tre minuti e quindi aggiornare la pagina, causando l'esecuzione di un evento di postback. Si noti che l'ora visualizzata nella pagina è cambiata. Se si aggiorna la pagina in meno di tre minuti, l'ora visualizzata nella pagina rimarrà invariata.  
  
Aggiornare ora i dati nel database usando un comando Transact-SQL UPDATE e aggiornare la pagina. L'ora visualizzata indica che la cache è stata aggiornata con i nuovi dati dal database. Si noti che anche se la cache viene aggiornata, l'ora visualizzata nella pagina non viene modificata fino a quando non si verifica un evento di postback.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Notifiche di query in SQL Server](query-notifications-sql-server.md)
