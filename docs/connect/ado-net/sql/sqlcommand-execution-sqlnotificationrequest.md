---
title: Esecuzione di SqlCommand con SqlNotificationRequest
description: Viene illustrata la configurazione di un oggetto SqlCommand per l'utilizzo di una notifica di query.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 892f11e2d81e3a0733a1f0747c0b72c72ebc79fc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451944"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>Esecuzione di SqlCommand con SqlNotificationRequest

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

È possibile configurare un <xref:Microsoft.Data.SqlClient.SqlCommand> per generare una notifica quando i dati vengono modificati dopo che sono stati recuperati dal server e il set di risultati è diverso se la query è stata eseguita di nuovo. Questa operazione è utile per gli scenari in cui si desidera utilizzare le code di notifica personalizzate sul server o quando non si desidera mantenere oggetti attivi.

## <a name="creating-the-notification-request"></a>Creazione della richiesta di notifica

Per creare la richiesta di notifica, è possibile utilizzare un oggetto <xref:Microsoft.Data.Sql.SqlNotificationRequest> associarlo a un oggetto `SqlCommand`. Una volta creata la richiesta, l'oggetto `SqlNotificationRequest` non è più necessario. È possibile eseguire una query sulla coda per eventuali notifiche e rispondere in modo appropriato. Le notifiche possono verificarsi anche se l'applicazione viene arrestata e successivamente riavviata.

Quando viene eseguito il comando con la notifica associata, le eventuali modifiche apportate al set di risultati originale attivano l'invio di un messaggio alla coda di SQL Server configurata nella richiesta di notifica.

Il polling della coda di SQL Server e l'interpretazione del messaggio sono specifici dell'applicazione. L'applicazione è responsabile del polling della coda e della reazione in base al contenuto del messaggio.

> [!NOTE]
> Quando si usano SQL Server richieste di notifica con <xref:Microsoft.Data.SqlClient.SqlDependency>, creare il proprio nome di coda invece di usare il nome del servizio predefinito.

Non sono presenti nuovi elementi di sicurezza sul lato client per <xref:Microsoft.Data.Sql.SqlNotificationRequest>. Si tratta principalmente di una funzionalità server e il server ha creato privilegi speciali che gli utenti devono avere per richiedere una notifica.

### <a name="example"></a>Esempio

Nel frammento di codice seguente viene illustrato come creare una <xref:Microsoft.Data.Sql.SqlNotificationRequest> e associarla a una <xref:Microsoft.Data.SqlClient.SqlCommand>.

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>Passaggi successivi
- [Notifiche di query in SQL Server](query-notifications-sql-server.md)
