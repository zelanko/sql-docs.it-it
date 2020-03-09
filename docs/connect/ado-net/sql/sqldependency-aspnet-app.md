---
title: SqlDependency in un'applicazione ASP.NET
description: Viene illustrato l'uso delle notifiche di query da un'applicazione ASP.NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 8e159a6db1820169cd81caa05e70765ac32f0d56
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896235"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency in un'applicazione ASP.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

L'esempio riportato in questa sezione illustra come usare <xref:Microsoft.Data.SqlClient.SqlDependency> indirettamente sfruttando l'oggetto ASP.NET <xref:System.Web.Caching.SqlCacheDependency>. L'oggetto <xref:System.Web.Caching.SqlCacheDependency> usa un <xref:Microsoft.Data.SqlClient.SqlDependency> per ascoltare le notifiche e aggiornare correttamente la cache.  
  
> [!NOTE]
>  Nell'esempio di codice si presuppone che le notifiche di query siano state abilitate eseguendo gli script descritti in [Abilitazione di notifiche di query](enable-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Informazioni sull'applicazione di esempio  
Nell'applicazione di esempio viene usata una singola pagina Web ASP.NET per visualizzare in un controllo <xref:System.Web.UI.WebControls.GridView> le informazioni sui prodotti disponibili nel database **AdventureWorks** di SQL Server. Quando la pagina viene caricata il codice scrive l'ora corrente in un controllo <xref:System.Web.UI.WebControls.Label>. Definisce quindi un oggetto <xref:System.Web.Caching.SqlCacheDependency> e imposta le proprietà nell'oggetto <xref:System.Web.Caching.Cache> per archiviare i dati della cache per un massimo di tre minuti. Il codice si connette quindi al database e recupera i dati. Quando la pagina viene caricata e l'applicazione è in esecuzione ASP.NET recupera i dati dalla cache ed è possibile verificarlo osservando che l'ora sulla pagina non cambia. Se i dati monitorati cambiano, ASP.NET invalida la cache e ripopola il controllo `GridView` con i dati aggiornati, adeguando l'ora visualizzata nel controllo `Label`.  
  
## <a name="creating-the-sample-application"></a>Creazione dell'applicazione di esempio  
Per creare ed eseguire l'applicazione di esempio, seguire questa procedura:  
  
1. Creare un nuovo sito Web ASP.NET.  
  
2. Aggiungere un <xref:System.Web.UI.WebControls.Label> e un controllo <xref:System.Web.UI.WebControls.GridView> alla pagina Default.aspx.  
  
3. Aprire il modulo di classe della pagina e aggiungere le direttive seguenti:  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Aggiungere il codice seguente all'evento `Page_Load` della pagina:  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. Aggiungere due metodi helper, `GetConnectionString` e `GetSQL`. La stringa di connessione definita usa la sicurezza integrata. Sarà necessario verificare che l'account in uso disponga delle autorizzazioni del database richieste e che siano abilitate le notifiche nel database di esempio **AdventureWorks**.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>Test dell'applicazione  
L'applicazione memorizza nella cache i dati visualizzati nel Web Form e li aggiorna ogni tre minuti se non è presente alcuna attività. Se viene apportata una modifica al database, la cache viene aggiornata immediatamente. Eseguire l'applicazione da Visual Studio, che carica la pagina nel browser. L'ora di aggiornamento della cache visualizzata indica il momento in cui la cache è stata aggiornata l'ultima volta. Attendere tre minuti e quindi aggiornare la pagina, causando l'esecuzione di un evento di postback. Si noti che l'ora visualizzata nella pagina è cambiata. Se si aggiorna la pagina in meno di tre minuti, l'ora visualizzata sulla pagina rimane invariata.  
  
A questo punto aggiornare i dati nel database usando un comando Transact-SQL UPDATE e aggiornare la pagina. L'ora visualizzata indica che la cache è stata aggiornata con i nuovi dati provenienti dal database. Si noti che sebbene la cache venga aggiornata, l'ora visualizzata sulla pagina non cambia finché non si verifica un evento di postback.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Notifiche di query in SQL Server](query-notifications-sql-server.md)
