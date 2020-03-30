---
title: Mirroring del database in SQL Server
description: Descrive la funzionalità di mirroring del database.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: c7ace2feb39bcc3f5f257c0ac2c7360649cfc33c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897005"
---
# <a name="database-mirroring-in-sql-server"></a>Mirroring del database in SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Il mirroring del database in SQL Server consente di mantenere una copia, o mirror, di un database di SQL Server in un server di standby. Il mirroring garantisce che siano sempre presenti due copie separate dei dati, offrendo disponibilità elevata e ridondanza completa dei dati. Il provider Microsoft SqlClient per SQL Server fornisce il supporto implicito per il mirroring del database. Pertanto, una volta configurato il provider per un database di SQL Server, lo sviluppatore non dovrà eseguire alcuna operazione né scrivere codice. L'oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> supporta inoltre una modalità di connessione esplicita che consente di specificare il nome di un server partner di failover in <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
Questa sequenza di eventi semplificata si verifica per un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> che ha come destinazione un database configurato per il mirroring:  
  
1. L'applicazione client si connette correttamente al database principale e il server restituisce il nome del server partner che viene quindi memorizzato nella cache del client.  
  
2. In caso di errore del server contenente il database principale o di interruzione della connettività, lo stato della connessione e della transazione andrà perso. L'applicazione client tenta di ristabilire una connessione al database principale e non riesce.  
  
3. L'applicazione client tenta quindi di stabilire in modo trasparente una connessione al database mirror nel server partner. Se l'esito è positivo, la connessione viene reindirizzata al database mirror che diventa quindi il nuovo database principale.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>Definizione del partner di failover nella stringa di connessione  
Se si specifica il nome di un server partner di failover nella stringa di connessione, il client tenterà di connettersi in modo trasparente al partner di failover se il database principale non è disponibile quando l'applicazione client si connette per la prima volta.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
Se si omette il nome del server partner di failover e il database principale non è disponibile quando l'applicazione client si connette per la prima volta, viene generata l'eccezione <xref:Microsoft.Data.SqlClient.SqlException>.  
  
Quando l'oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> viene aperto, il server restituisce il nome del partner di failover che sostituirà tutti i valori specificati nella stringa di connessione.  
  
> [!NOTE]
>  Per gli scenari di mirroring del database, nella stringa di connessione è necessario specificare in modo esplicito il nome del catalogo o del database iniziale. Se il client riceve informazioni di failover su una connessione che non presenta un catalogo o un database iniziale specificato in modo esplicito, tali informazioni non vengono memorizzate nella cache e l'applicazione non tenta di eseguire il failover se si verifica un errore nel server principale. Se una stringa di connessione ha un valore per il partner di failover, ma nessun valore per il catalogo o il database iniziale, viene generata l'eccezione `InvalidArgumentException`.  
  
## <a name="retrieving-the-current-server-name"></a>Recupero del nome del server corrente  
In caso di failover, è possibile recuperare il nome del server al quale la connessione corrente è effettivamente connessa tramite la proprietà <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> di un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection>. Il frammento di codice seguente recupera il nome del server attivo, supponendo che la variabile di connessione faccia riferimento a un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> aperto.  
  
Quando si verifica un evento di failover e la connessione passa al server mirror, la proprietà **DataSource** viene aggiornata in modo da riflettere il nome del mirror.  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>Comportamento di mirroring di SqlClient  
Il client prova sempre a connettersi al server principale corrente. Se non riesce, prova a connettersi al partner di failover. Se il database mirror è stato già passato al ruolo principale nel server partner, la connessione riesce e il nuovo mapping ruolo principale-mirror viene inviato al client e memorizzato nella cache per la durata dell'oggetto <xref:System.AppDomain> chiamante. Il nuovo mapping non viene memorizzato nell'archivio permanente e non è disponibile per successive connessioni in un **AppDomain** o in un processo diverso. È disponibile, tuttavia, per connessioni successive all'interno dello stesso **AppDomain**. Notare che un **AppDomain** o un processo diverso eseguito sullo stesso computer o su un computer diverso dispone sempre del proprio pool di connessioni e tali connessioni non vengono reimpostate. In questo caso, se il database primario diventa inattivo, ogni processo o **AppDomain** ha esito negativo una volta e il pool viene cancellato automaticamente.  
  
> [!NOTE]
>  Il supporto del mirroring nel server viene configurato per ogni database. Se vengono eseguite operazioni di manipolazione dei dati su altri database non inclusi nel set principale/mirror, usando nomi multipart o modificando il database corrente, le modifiche apportate a questi altri database non vengono propagate in caso di errore. Quando si modificano i dati in un database senza mirroring, non viene generato alcun errore. Lo sviluppatore deve valutare il possibile impatto di queste operazioni.  
  
## <a name="next-steps"></a>Passaggi successivi
### <a name="database-mirroring-resources"></a>Risorse per il mirroring del database  
Per informazioni di carattere concettuale e sulla configurazione, la distribuzione e l'amministrazione del mirroring, vedere le risorse seguenti nella documentazione di SQL Server.  
  
|Risorsa|Descrizione|  
|--------------|-----------------|  
|[Mirroring del database](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|Viene descritto come impostare e configurare il mirroring in SQL Server.|  
