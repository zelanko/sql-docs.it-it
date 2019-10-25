---
title: Mirroring del database in SQL Server
description: Viene descritta la funzionalità di mirroring del database.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 1c78f52f376ff6c333b952b8d013e17eefce45ea
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452269"
---
# <a name="database-mirroring-in-sql-server"></a>Mirroring del database in SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Il mirroring del database in SQL Server consente di mantenere una copia, o mirror, di un database di SQL Server in un server di standby. Il mirroring garantisce che siano sempre presenti due copie separate dei dati, garantendo disponibilità elevata e ridondanza dei dati completa. Il provider Microsoft SqlClient per SQL Server fornisce il supporto implicito per il mirroring del database. Pertanto, una volta configurato il provider per un database di SQL Server, lo sviluppatore non dovrà eseguire alcuna operazione né scrivere codice. Inoltre, l'oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> supporta una modalità di connessione esplicita che consente di specificare il nome di un server partner di failover nel <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
La seguente sequenza semplificata di eventi si verifica per un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> destinato a un database configurato per il mirroring:  
  
1. L'applicazione client esegue correttamente la connessione al database principale e il server restituisce il nome del server partner, che viene quindi memorizzato nella cache del client.  
  
2. Se il server che contiene il database principale ha esito negativo o viene interrotta la connettività, lo stato della connessione e della transazione viene perso. L'applicazione client tenta di ristabilire una connessione al database principale e ha esito negativo.  
  
3. L'applicazione client tenta in modo trasparente di stabilire una connessione al database mirror nel server partner. In caso di esito positivo, la connessione viene reindirizzata al database mirror, che diventa il nuovo database principale.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>Impostazione del partner di failover nella stringa di connessione  
Se si specifica il nome di un server partner di failover nella stringa di connessione, il client tenterà in modo trasparente la connessione al partner di failover se il database principale non è disponibile quando l'applicazione client si connette per la prima volta.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
Se si omette il nome del server partner di failover e il database principale non è disponibile quando l'applicazione client si connette per la prima volta, viene generata un'<xref:Microsoft.Data.SqlClient.SqlException>.  
  
Quando un <xref:Microsoft.Data.SqlClient.SqlConnection> viene aperto correttamente, il nome del partner di failover viene restituito dal server e sostituisce tutti i valori specificati nella stringa di connessione.  
  
> [!NOTE]
>  È necessario specificare in modo esplicito il nome del catalogo o del database iniziale nella stringa di connessione per gli scenari di mirroring del database. Se il client riceve informazioni di failover su una connessione che non presenta un catalogo o un database iniziale specificato in modo esplicito, tali informazioni non vengono memorizzate nella cache e l'applicazione non tenta di eseguire il failover se si verifica un errore nel server principale. Se una stringa di connessione dispone di un valore per il partner di failover, ma non di un valore per il catalogo o il database iniziale, viene generata un'`InvalidArgumentException`.  
  
## <a name="retrieving-the-current-server-name"></a>Recupero del nome del server corrente  
In caso di failover, è possibile recuperare il nome del server al quale la connessione corrente è effettivamente connessa tramite la proprietà <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> di un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection>. Il frammento di codice seguente recupera il nome del server attivo, supponendo che la variabile di connessione faccia riferimento a un <xref:Microsoft.Data.SqlClient.SqlConnection> aperto.  
  
Quando si verifica un evento di failover e la connessione viene spostata sul server mirror, la proprietà **DataSource** viene aggiornata per riflettere il nome del mirror.  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>Comportamento di mirroring SqlClient  
Il client tenta sempre di connettersi al server principale corrente. Se ha esito negativo, tenta il partner di failover. Se il database mirror è già stato impostato sul ruolo principale nel server partner, la connessione ha esito positivo e il nuovo mapping principale-mirror viene inviato al client e memorizzato nella cache per la durata del <xref:System.AppDomain> chiamante. Il nuovo mapping non viene memorizzato nell'archivio permanente e non è disponibile per successive connessioni in un **AppDomain** o in un processo diverso. È disponibile, tuttavia, per connessioni successive all'interno dello stesso **AppDomain**. Notare che un **AppDomain** o un processo diverso eseguito sullo stesso computer o su un computer diverso dispone sempre del proprio pool di connessioni e tali connessioni non vengono reimpostate. In questo caso, se il database primario diventa inattivo, ogni processo o **AppDomain** ha esito negativo una volta e il pool viene cancellato automaticamente.  
  
> [!NOTE]
>  Il supporto per il mirroring nel server viene configurato per ogni singolo database. Se le operazioni di manipolazione dei dati vengono eseguite su altri database non inclusi nel set principale/mirror, utilizzando nomi multipart o modificando il database corrente, le modifiche apportate a questi database non vengono propagate in caso di errore. Non viene generato alcun errore quando i dati vengono modificati in un database di cui non è stato creato il mirroring. Lo sviluppatore deve valutare il possibile effetto di tali operazioni.  
  
## <a name="next-steps"></a>Passaggi successivi
### <a name="database-mirroring-resources"></a>Risorse per il mirroring del database  
Per informazioni di carattere concettuale e sulla configurazione, la distribuzione e l'amministrazione del mirroring, vedere le risorse seguenti nella documentazione di SQL Server.  
  
|Risorsa|Descrizione|  
|--------------|-----------------|  
|[Mirroring del database](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|Viene descritto come impostare e configurare il mirroring in SQL Server.|  
