---
title: Abilitazione di MARS (Multiple Active Result Set)
description: Viene descritto come usare MARS con SQL Server.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: feeca1a8bac8b4e1ec55cda0e025ca4b26a94c20
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920432"
---
# <a name="enabling-multiple-active-result-sets"></a>Abilitazione di MARS (Multiple Active Result Set)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

MARS (Multiple Active Result Set) è un servizio che funziona in combinazione con SQL Server per consentire l'esecuzione di più batch in un'unica connessione. Quando MARS è abilitato per l'uso con SQL Server, ciascun oggetto comando usato aggiunge una sessione alla connessione.  
  
> [!NOTE]
>  Una singola sessione MARS apre una connessione logica per l'uso da parte di MARS e quindi una connessione logica per ogni comando attivo.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>Abilitazione e disabilitazione di MARS nella stringa di connessione  
  
> [!NOTE]
>  Le stringhe di connessione seguenti usano il database di esempio **AdventureWorks** incluso in SQL Server. Le stringhe di connessione specificate presuppongono che il database sia installato in un server denominato MSSQL1. Modificare la stringa di connessione in base alle esigenze dell'ambiente in uso.  
  
La funzionalità MARS è disabilitata per impostazione predefinita. Può essere abilitata aggiungendo la coppia di parole chiave "MultipleActiveResultSets=True" alla stringa di connessione. "True" è l'unico valore valido per l'abilitazione di MARS. L'esempio seguente illustra come connettersi a un'istanza di SQL Server e specificare che MARS deve essere abilitato. 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
Per disabilitare MARS, aggiungere la coppia di parole chiave "MultipleActiveResultSets=False" alla stringa di connessione. "False" è l'unico valore valido per la disabilitazione di MARS. La stringa di connessione seguente illustra come disabilitare MARS.  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>Considerazioni speciali sull'uso di MARS  
In generale, non è necessario modificare le applicazioni esistenti per usare una connessione abilitata per MARS. Tuttavia, per usare le funzionalità MARS nelle proprie applicazioni, è importante comprendere le considerazioni speciali riportate di seguito.  
  
### <a name="statement-interleaving"></a>Interfoliazione di istruzioni  
Le operazioni MARS vengono eseguite in modo sincrono sul server. È consentita l'interfoliazione delle istruzioni SELECT e BULK INSERT. Tuttavia, le istruzioni DML (Data Manipulation Language) e DDL (Data Definition Language) vengono eseguite in modo atomico. Eventuali istruzioni che tentano l'esecuzione mentre viene eseguito un batch atomico vengono bloccate. L'esecuzione parallela sul server non è una funzionalità MARS.  
  
Se si usa una connessione MARS per inviare due batch, uno contenente un'istruzione SELECT e l'altro contenente un'istruzione DML, l'istruzione DML può iniziare l'esecuzione all'interno dell'esecuzione dell'istruzione SELECT. Tuttavia, è necessario che l'istruzione DML venga eseguita fino in fondo prima che l'istruzione SELECT possa avanzare. Se entrambe le istruzioni vengono eseguite nella stessa transazione, eventuali modifiche apportate da un'istruzione DML dopo l'avvio dell'esecuzione dell'istruzione SELECT non sono visibili all'operazione di lettura.  
  
Un'istruzione WAITFOR all'interno di un'istruzione SELECT non sospende la transazione mentre è in attesa, ovvero finché viene prodotta la prima riga. Ciò implica che non è possibile eseguire altri batch nella stessa connessione mentre è in attesa un'istruzione WAITFOR.  
  
### <a name="mars-session-cache"></a>Cache della sessione MARS  
Quando viene aperta una connessione con MARS abilitato, viene creata una sessione logica che aggiunge ulteriore overhead. Per ridurre al minimo l'overhead e migliorare le prestazioni, **SqlClient** memorizza nella cache la sessione MARS all'interno di una connessione. La cache contiene al massimo 10 sessioni MARS. Questo valore non può essere modificato dall'utente. Se viene raggiunto il limite della sessione, viene creata una nuova sessione, non viene generato un errore. La cache e le sessioni contenute nella stessa sono specifiche di una connessione e non vengono condivise tra le connessioni. Quando una sessione viene rilasciata, viene restituita al pool, a meno che non sia stato raggiunto il limite massimo del pool. Se il pool di cache è pieno, la sessione viene chiusa. Le sessioni MARS non scadono. Vengono solo pulite quando l'oggetto connessione viene eliminato. La cache della sessione MARS non è precaricata. Viene caricata nel momento in cui l'applicazione richiede più sessioni.  
  
### <a name="thread-safety"></a>Thread safety  
Le operazioni MARS non sono thread-safe.  
  
### <a name="connection-pooling"></a>Pool di connessioni  
Le connessioni con supporto per MARS sono in pool come qualsiasi altra connessione. Se un'applicazione apre due connessioni, una con MARS abilitato e una con MARS disabilitato, le due connessioni sono in pool separati.
  
### <a name="sql-server-batch-execution-environment"></a>Ambiente di esecuzione batch di SQL Server  
Quando si apre una connessione si definisce un ambiente predefinito. Questo ambiente successivamente viene copiato in una sessione MARS logica.  
  
L'ambiente di esecuzione batch include i componenti seguenti:  
  
- Opzioni SET (ad esempio ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)  
  
- Contesto di protezione (ruolo utente/applicazione)  
  
- Contesto del database (database corrente)  
  
- Variabili dello stato di esecuzione (ad esempio @@ERROR, @@ROWCOUNT, @@FETCH_STATUS @@IDENTITY)  
  
- Tabelle temporanee di livello principale  
  
Con MARS, un ambiente di esecuzione predefinito viene associato a una connessione. Ogni nuovo batch per cui viene avviata l'esecuzione nell'ambito di una connessione specifica riceve una copia dell'ambiente predefinito. Ogni volta che il codice viene eseguito in un determinato batch, tutte le modifiche apportate all'ambiente hanno come ambito il batch specifico. Al termine dell'esecuzione, le impostazioni di esecuzione vengono copiate nell'ambiente predefinito. Nel caso di un singolo batch che prevede più comandi da eseguire in modo sequenziale nella stessa transazione, la semantica corrisponde a quella delle connessioni che includono client e server di versioni precedenti.  
  
### <a name="parallel-execution"></a>Esecuzione parallela  
MARS non è progettato per rimuovere tutti i requisiti per più connessioni in un'applicazione. Se un'applicazione richiede un'effettiva esecuzione parallela dei comandi su un server, è necessario usare più connessioni.  
  
Ad esempio, si consideri lo scenario seguente. Vengono creati due oggetti comando, uno per l'elaborazione di un set di risultati e un altro per l'aggiornamento dei dati. I due oggetti condividono una connessione comune via MARS. In questo scenario con `Transaction`.`Commit` l'aggiornamento non ha esito positivo finché non vengono letti tutti i risultati sul primo oggetto comando, restituendo l'eccezione seguente:  
  
Messaggio: Il contesto della transazione è in uso in un'altra sessione.  
  
Origine: Microsoft SqlClient Data Provider  
  
Previsto: (null)  
  
Ricevuto: Microsoft.Data.SqlClient.SqlException  
  
Sono disponibili tre opzioni per la gestione di questo scenario:  
  
- Avviare la transazione dopo la creazione del lettore, in modo che non faccia parte della transazione. Ogni aggiornamento diventa quindi la propria transazione.  
  
- Eseguire il commit di tutto il lavoro dopo la chiusura del lettore. Questo può comportare un notevole batch di aggiornamenti.  
  
- Non usare MARS, usare invece una connessione separata per ogni oggetto comando come era consueto fare prima di MARS.  
  
### <a name="detecting-mars-support"></a>Rilevamento del supporto di MARS  
Un'applicazione può verificare la disponibilità del supporto di MARS leggendo il valore `SqlConnection.ServerVersion`. Il numero massimo deve essere 9 per SQL Server 2005 il 10 per SQL Server 2008.  
  
## <a name="next-steps"></a>Passaggi successivi
- [MARS (Multiple Active Result Sets)](multiple-active-result-sets-mars.md)
