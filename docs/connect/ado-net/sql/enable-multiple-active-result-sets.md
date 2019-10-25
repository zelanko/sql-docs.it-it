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
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452224"
---
# <a name="enabling-multiple-active-result-sets"></a>Abilitazione di MARS (Multiple Active Result Set)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

MARS (Multiple Active Result Set) è un servizio che funziona in combinazione con SQL Server per consentire l'esecuzione di più batch in un'unica connessione. Quando MARS è abilitato per l'uso con SQL Server, ciascun oggetto comando usato aggiunge una sessione alla connessione.  
  
> [!NOTE]
>  Una singola sessione MARS apre una connessione logica per Marte da usare e quindi una connessione logica per ogni comando attivo.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>Abilitazione e disabilitazione di MARS nella stringa di connessione  
  
> [!NOTE]
>  Le stringhe di connessione seguenti usano il database di esempio **AdventureWorks** incluso in SQL Server. Le stringhe di connessione fornite presuppongono che il database sia installato in un server denominato MSSQL1. Modificare la stringa di connessione in modo che sia necessario per l'ambiente in uso.  
  
La funzionalità MARS è disabilitata per impostazione predefinita. Può essere abilitata aggiungendo la coppia di parole chiave "MultipleActiveResultSets = true" alla stringa di connessione. "True" è l'unico valore valido per l'abilitazione di MARS. Nell'esempio seguente viene illustrato come connettersi a un'istanza di SQL Server e come specificare che MARS deve essere abilitato. 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
È possibile disabilitare MARS aggiungendo la coppia di parole chiave "MultipleActiveResultSets = False" alla stringa di connessione. "False" è l'unico valore valido per la disabilitazione di MARS. Nella stringa di connessione seguente viene illustrato come disabilitare MARS.  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>Considerazioni speciali quando si usa MARS  
In generale, non è necessario modificare le applicazioni esistenti per usare una connessione abilitata per MARS. Tuttavia, se si desidera utilizzare le funzionalità MARS nelle applicazioni, è necessario comprendere le considerazioni speciali seguenti.  
  
### <a name="statement-interleaving"></a>Interfoliazione di istruzioni  
Le operazioni MARS vengono eseguite in modo sincrono sul server. È consentita l'interfoliazione dell'istruzione SELECT e BULK INSERT. Tuttavia, le istruzioni Data Manipulation Language (DML) e Data Definition Language (DDL) vengono eseguite atomicamente. Eventuali istruzioni che tentano di eseguire durante l'esecuzione di un batch atomico sono bloccate. L'esecuzione parallela nel server non è una funzionalità MARS.  
  
Se due batch vengono inviati in una connessione MARS, uno dei quali contiene un'istruzione SELECT, l'altro contenente un'istruzione DML, il DML può iniziare l'esecuzione all'interno dell'esecuzione dell'istruzione SELECT. Tuttavia, è necessario che l'istruzione DML venga completata prima che l'istruzione SELECT possa avanzare. Se entrambe le istruzioni sono in esecuzione nella stessa transazione, le modifiche apportate da un'istruzione DML dopo l'avvio dell'esecuzione dell'istruzione SELECT non saranno visibili all'operazione di lettura.  
  
Un'istruzione Wait all'interno di un'istruzione SELECT non restituisce la transazione mentre è in attesa, ovvero fino a quando non viene prodotta la prima riga. Ciò implica che non è possibile eseguire altri batch nella stessa connessione mentre un'istruzione Wait è in attesa.  
  
### <a name="mars-session-cache"></a>Cache della sessione MARS  
Quando viene aperta una connessione con MARS abilitato, viene creata una sessione logica che aggiunge un sovraccarico aggiuntivo. Per ridurre al minimo l'overhead e migliorare le prestazioni, **SqlClient** memorizza nella cache la sessione MARS all'interno di una connessione. La cache contiene al massimo 10 sessioni MARS. Questo valore non è modificabile dall'utente. Se viene raggiunto il limite della sessione, viene creata una nuova sessione, ovvero non viene generato un errore. La cache e le sessioni contenute sono per connessione; non sono condivise tra le connessioni. Quando una sessione viene rilasciata, viene restituita al pool, a meno che non sia stato raggiunto il limite massimo del pool. Se il pool di cache è pieno, la sessione viene chiusa. Le sessioni MARS non scadono. Vengono puliti solo quando l'oggetto connessione viene eliminato. La cache della sessione MARS non è precaricata. Viene caricato perché l'applicazione richiede più sessioni.  
  
### <a name="thread-safety"></a>Thread safety  
Le operazioni MARS non sono thread-safe.  
  
### <a name="connection-pooling"></a>Pool di connessioni  
Le connessioni abilitate per MARS sono in pool come qualsiasi altra connessione. Se un'applicazione apre due connessioni, una con MARS abilitato e una con MARS disabilitata, le due connessioni si trovano in pool distinti.
  
### <a name="sql-server-batch-execution-environment"></a>Ambiente di esecuzione batch SQL Server  
Quando viene aperta una connessione, viene definito un ambiente predefinito. Questo ambiente viene quindi copiato in una sessione MARS logica.  
  
L'ambiente di esecuzione batch include i componenti seguenti:  
  
- Opzioni set (ad esempio, ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)  
  
- Contesto di sicurezza (ruolo utente/applicazione)  
  
- Contesto di database (database corrente)  
  
- Variabili dello stato di esecuzione (ad esempio, @ @ERROR, @ @ROWCOUNT, @ @FETCH_STATUS @ @IDENTITY)  
  
- Tabelle temporanee di livello principale  
  
Con MARS, un ambiente di esecuzione predefinito è associato a una connessione. Ogni nuovo batch per cui viene avviata l'esecuzione nell'ambito di una connessione specifica riceve una copia dell'ambiente predefinito. Ogni volta che il codice viene eseguito in un determinato batch, tutte le modifiche apportate all'ambiente hanno come ambito il batch specifico. Al termine dell'esecuzione, le impostazioni di esecuzione vengono copiate nell'ambiente predefinito. Nel caso di un singolo batch che emette diversi comandi da eseguire in sequenza nella stessa transazione, la semantica è identica a quella esposta dalle connessioni che coinvolgono client o server precedenti.  
  
### <a name="parallel-execution"></a>Esecuzione parallela  
MARS non è progettato per rimuovere tutti i requisiti per più connessioni in un'applicazione. Se per un'applicazione è necessaria l'esecuzione parallela effettiva di comandi su un server, è necessario usare più connessioni.  
  
Si consideri, ad esempio, lo scenario seguente. Vengono creati due oggetti comando, uno per l'elaborazione di un set di risultati e un altro per l'aggiornamento dei dati; condividono una connessione comune tramite MARS. In questo scenario con `Transaction`.`Commit` l'aggiornamento non ha esito positivo finché non vengono letti tutti i risultati sul primo oggetto comando, restituendo l'eccezione seguente:  
  
Messaggio: Il contesto della transazione è in uso in un'altra sessione.  
  
Origine: Microsoft SqlClient provider di dati  
  
Previsto: (null)  
  
Ricevuto: Microsoft. Data. SqlClient. SqlException  
  
Sono disponibili tre opzioni per la gestione di questo scenario:  
  
- Avviare la transazione dopo la creazione del lettore, in modo che non faccia parte della transazione. Ogni aggiornamento diventa quindi la propria transazione.  
  
- Eseguire il commit di tutto il lavoro dopo la chiusura del lettore. Questo può comportare un notevole batch di aggiornamenti.  
  
- Non usare MARS; usare invece una connessione separata per ogni oggetto Command come si farebbe prima di MARS.  
  
### <a name="detecting-mars-support"></a>Rilevamento del supporto di MARS  
Un'applicazione può verificare il supporto per MARS leggendo il valore `SqlConnection.ServerVersion`. Il numero principale deve essere 9 per SQL Server 2005 e 10 per SQL Server 2008.  
  
## <a name="next-steps"></a>Passaggi successivi
- [MARS (Multiple Active Result Sets)](multiple-active-result-sets-mars.md)
