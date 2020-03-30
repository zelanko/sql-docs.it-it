---
title: Rilevamento di modifiche con SqlDependency
description: Illustra come rilevare i casi in cui i risultati della query si differenziano da quelli ricevuti in origine.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 90b11516e9fa8ed993792bfec2a77757249b696d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896983"
---
# <a name="detecting-changes-with-sqldependency"></a>Rilevamento di modifiche con SqlDependency

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Un oggetto <xref:Microsoft.Data.SqlClient.SqlDependency> può essere associato a un <xref:Microsoft.Data.SqlClient.SqlCommand> per scoprire quando i risultati della query presentano delle differenze rispetto a quelli recuperati in origine. È anche possibile assegnare un delegato all'evento `OnChange`, che verrà attivato quando i risultati cambiano per un comando associato. Prima di eseguire il comando, è necessario associare <xref:Microsoft.Data.SqlClient.SqlDependency> al comando. È inoltre possibile usare la proprietà `HasChanges` di <xref:Microsoft.Data.SqlClient.SqlDependency> per determinare se i risultati della query sono cambiati dopo il primo recupero dei dati.

## <a name="security-considerations"></a>Considerazioni relative alla sicurezza

L'infrastruttura di dipendenza si basa su un <xref:Microsoft.Data.SqlClient.SqlConnection> aperto quando si chiama <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> per ricevere le notifiche relative alla modifica dei dati sottostanti per un determinato comando. La possibilità per un client di avviare la chiamata a `SqlDependency.Start` viene controllata usando <xref:Microsoft.Data.SqlClient.SqlClientPermission> e gli attributi di sicurezza dall'accesso di codice. Per altre informazioni, vedere [Abilitazione di notifiche di query](enable-query-notifications.md).

### <a name="example"></a>Esempio

Nei passaggi seguenti viene illustrato come dichiarare una dipendenza, eseguire un comando e ricevere una notifica quando il set di risultati cambia:

1. Attivar una connessione `SqlDependency` al server.

2. Creare gli oggetti <xref:Microsoft.Data.SqlClient.SqlConnection> e <xref:Microsoft.Data.SqlClient.SqlCommand> per connettersi al server e definire un'istruzione Transact-SQL.

3. Creare un nuovo oggetto `SqlDependency`, o usarne uno esistente, e associarlo all'oggetto `SqlCommand`. Internamente viene creato un oggetto <xref:Microsoft.Data.Sql.SqlNotificationRequest> che viene poi associato all'oggetto comando in base alle esigenze. Questa richiesta di notifica contiene un identificatore interno che identifica in modo univoco l'oggetto `SqlDependency`. Avvia anche il listener client, se non è già attivo.

4. Sottoscrivere un gestore eventi per l'evento `OnChange` dell'oggetto `SqlDependency`.

5. Eseguire il comando usando uno dei metodi `Execute` dell'oggetto `SqlCommand`. Poiché il comando è associato all'oggetto notifica, il server riconosce che deve generare una notifica e le informazioni sulla coda punteranno alla coda delle dipendenze.

6. Interrompere la connessione `SqlDependency` al server.

Se un utente successivamente modifica i dati sottostanti, Microsoft SQL Server rileva la presenza di una notifica in sospeso per tale modifica e invia una notifica, che viene elaborata e inoltrata al client usando l'oggetto `SqlConnection` sottostante creato con la chiamata a `SqlDependency.Start`. Il listener client riceve il messaggio di invalidamento, quindi individua l'oggetto `SqlDependency` associato e genera l'evento `OnChange`.

Il frammento di codice seguente illustra lo schema progettuale da usare per creare un'applicazione di esempio.

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="next-steps"></a>Passaggi successivi
- [Notifiche di query in SQL Server](query-notifications-sql-server.md)
