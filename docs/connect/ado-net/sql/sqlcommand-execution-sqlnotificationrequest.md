---
title: Esecuzione di SqlCommand con SqlNotificationRequest
description: Viene illustrata la configurazione di un oggetto SqlCommand per l'uso con una notifica di query.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: b4ec71c2bd693599106692a45f9e9aa10a63babd
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896233"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>Esecuzione di SqlCommand con SqlNotificationRequest

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

È possibile configurare un elemento <xref:Microsoft.Data.SqlClient.SqlCommand> per generare una notifica se i dati cambiano dopo essere stati recuperati dal server e il set di risultati è diverso se la query viene eseguita di nuovo. Questa operazione è utile per gli scenari in cui si usano code di notifica personalizzate sul server o non si vogliono gestire oggetti attivi.

## <a name="creating-the-notification-request"></a>Creazione della richiesta di notifica

Per creare la richiesta di notifica, è possibile usare un oggetto <xref:Microsoft.Data.Sql.SqlNotificationRequest> associandolo a un oggetto `SqlCommand`. Dopo la creazione della richiesta, l'oggetto `SqlNotificationRequest` non è più necessario. È possibile eseguire una query sulla coda per verificare la presenza di notifiche e rispondere in modo appropriato. Le notifiche possono verificarsi anche se l'applicazione viene arrestata e successivamente riavviata.

Quando viene eseguito il comando con la notifica associata, le eventuali modifiche apportate al set di risultati originale attivano l'invio di un messaggio alla coda di SQL Server configurata nella richiesta di notifica.

Il polling della coda di SQL Server e l'interpretazione del messaggio sono specifici dell'applicazione. L'applicazione è responsabile del polling della coda e della reazione in base al contenuto del messaggio.

> [!NOTE]
> Quando si usano le richieste di notifica di SQL Server con <xref:Microsoft.Data.SqlClient.SqlDependency>, creare il proprio nome di coda invece di usare il nome del servizio predefinito.

Non esistono nuovi elementi di sicurezza sul lato client per <xref:Microsoft.Data.Sql.SqlNotificationRequest>. Questa è principalmente una funzionalità server e il server ha creato privilegi speciali che gli utenti devono avere per richiedere una notifica.

### <a name="example"></a>Esempio

Il frammento di codice seguente illustra come creare un elemento <xref:Microsoft.Data.Sql.SqlNotificationRequest> e associarlo a un elemento <xref:Microsoft.Data.SqlClient.SqlCommand>.

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
