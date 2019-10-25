---
title: Rilevamento di modifiche con SqlDependency
description: Viene illustrato come rilevare quando i risultati della query saranno diversi da quelli ricevuti originariamente.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2d2c4c48a9085fa83d6104233be5f2e1c6b11318
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452239"
---
# <a name="detecting-changes-with-sqldependency"></a>Rilevamento di modifiche con SqlDependency

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Un oggetto <xref:Microsoft.Data.SqlClient.SqlDependency> può essere associato a un <xref:Microsoft.Data.SqlClient.SqlCommand> per rilevare quando i risultati della query sono diversi da quelli recuperati in origine. È anche possibile assegnare un delegato all'evento `OnChange`, che viene attivato quando i risultati cambiano per un comando associato. Prima di eseguire il comando, è necessario associare il <xref:Microsoft.Data.SqlClient.SqlDependency> al comando. È inoltre possibile utilizzare la proprietà `HasChanges` della <xref:Microsoft.Data.SqlClient.SqlDependency> per determinare se i risultati della query sono stati modificati dopo la prima volta che i dati sono stati recuperati.

## <a name="security-considerations"></a>Considerazioni sulla sicurezza

L'infrastruttura di dipendenza si basa su un <xref:Microsoft.Data.SqlClient.SqlConnection> aperto quando viene chiamato <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> per ricevere le notifiche relative alla modifica dei dati sottostanti per un determinato comando. La possibilità per un client di avviare la chiamata a `SqlDependency.Start` viene controllata tramite l'utilizzo di <xref:Microsoft.Data.SqlClient.SqlClientPermission> e degli attributi di sicurezza per l'accesso di codice. Per ulteriori informazioni, vedere [Abilitazione delle notifiche delle query](enable-query-notifications.md).

### <a name="example"></a>Esempio

Nei passaggi seguenti viene illustrato come dichiarare una dipendenza, eseguire un comando e ricevere una notifica quando il set di risultati cambia:

1. Attivar una connessione `SqlDependency` al server.

2. Creare <xref:Microsoft.Data.SqlClient.SqlConnection> e <xref:Microsoft.Data.SqlClient.SqlCommand> oggetti per connettersi al server e definire un'istruzione Transact-SQL.

3. Creare un nuovo oggetto `SqlDependency` o utilizzarne uno esistente e associarlo all'oggetto `SqlCommand`. Internamente, viene creato un oggetto <xref:Microsoft.Data.Sql.SqlNotificationRequest> e associato all'oggetto Command in base alle esigenze. Questa richiesta di notifica contiene un identificatore interno che identifica in modo univoco questo oggetto `SqlDependency`. Avvia anche il listener client, se non è già attivo.

4. Sottoscrivere un gestore eventi per l'evento `OnChange` dell'oggetto `SqlDependency`.

5. Eseguire il comando usando uno dei metodi di `Execute` dell'oggetto `SqlCommand`. Poiché il comando è associato all'oggetto notifica, il server riconosce che deve generare una notifica e le informazioni della coda punteranno alla coda delle dipendenze.

6. Arrestare la connessione `SqlDependency` al server.

Se un utente modifica successivamente i dati sottostanti, Microsoft SQL Server rileva la presenza di una notifica in sospeso per tale modifica e invia una notifica che viene elaborata e inoltrata al client tramite la `SqlConnection` sottostante creata da chiamata di `SqlDependency.Start`. Il listener client riceve il messaggio di invalidamento. Il listener client individua quindi l'oggetto `SqlDependency` associato e genera l'evento `OnChange`.

Il frammento di codice seguente illustra il modello di progettazione da usare per creare un'applicazione di esempio.

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
