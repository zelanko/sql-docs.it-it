---
title: Creare applicazioni client per dati FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20573362cc8eb41c3b6741bbc6efb8f6a3f9c9f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094282"
---
# <a name="create-client-applications-for-filestream-data"></a>Creazione di applicazioni client per dati FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le API Win32 consentono di leggere e scrivere dati in un oggetto BLOB FILESTREAM. È necessario effettuare le operazioni seguenti:  
  
-   Leggere il percorso del file FILESTREAM.  
  
-   Leggere il contesto di transazione corrente.  
  
-   Ottenere un handle Win32 e utilizzarlo per leggere e scrivere dati in un oggetto BLOB FILESTREAM.  
  
> [!NOTE]  
>  Gli esempi riportati in questo argomento richiedono il database e la tabella abilitati per FILESTREAM creati in [Creare un database abilitato per FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md) e [Creare una tabella per archiviare dati FILESTREAM](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md).  
  
##  <a name="func"></a> Funzioni per l'utilizzo di Dati FILESTREAM  
 Se si utilizza FILESTREAM per archiviare dati di oggetti binari di grandi dimensioni (BLOB), è possibile utilizzare API Win32 per usare i file. Per supportare l'utilizzo dei dati BLOB FILESTREAM nelle applicazioni Win32, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce le seguenti funzioni e API:  
  
-   [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) restituisce un percorso come token a un BLOB. In un'applicazione viene utilizzato questo token per ottenere un handle Win32 e operare sui dati BLOB.  
  
     Quando il database che contiene dati FILESTREAM appartiene a un gruppo di disponibilità Always On e la funzione PathName restituire un nome di rete virtuale (VNN) invece di un nome computer.  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) restituisce un token che rappresenta la transazione corrente di una sessione. In un'applicazione viene utilizzato questo token per associare le operazioni di flusso file system FILESTREAM alla transazione.  
  
-   Un handle di file Win32 è ottenuto in [API OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) . L'applicazione usa l'handle per trasmettere i dati FILESTREAM e può passare l'handle alle API Win32 seguenti: [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)o [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427). Se l'applicazione chiama qualsiasi altra API utilizzando l'handle, viene restituito un errore ERROR_ACCESS_DENIED. L'applicazione deve chiudere l'handle usando [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428).  
  
 L'accesso al contenitore di tutti i dati FILESTREAM viene eseguito in una transazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[tsql](../../includes/tsql-md.md)] possono essere eseguite nella stessa transazione per mantenere la coerenza tra i dati SQL e i dati FILESTREAM.  
  
##  <a name="steps"></a> Passaggi per l'accesso a dati FILESTREAM  
  
###  <a name="path"></a> Lettura del percorso del file FILESTREAM  
 A ogni cella di una tabella FILESTREAM è associato un percorso del file. Per leggere il percorso, usare la proprietà **PathName** di una colonna **varbinary(max)** in un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . L'esempio seguente illustra come leggere il percorso del file di una colonna **varbinary(max)** .  
  
 [!code-sql[FILESTREAM#FS_PathName](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_1.sql)]  
  
###  <a name="trx"></a> Lettura del contesto di transazione  
 Per ottenere il contesto di transazione corrente, usare la funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) . Nell'esempio seguente si illustra come iniziare una transazione e come leggere il contesto di transazione corrente.  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_2.sql)]  
  
###  <a name="handle"></a> Ottenere un handle di file Win32  
 Per ottenere un handle di file Win32, chiamare l'API OpenSqlFilestream. Tale API viene esportata dal file sqlncli.dll. L'handle restituito può essere passato a una qualsiasi delle API Win32 seguenti: [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)o [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427). Negli esempi seguenti si illustra come ottenere un handle di file Win32 e come utilizzarlo per leggere e scrivere dati in un oggetto BLOB FILESTREAM.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/create-client-applicatio_3.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/create-client-applicatio_4.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/create-client-applicatio_5.cpp)]  
  
##  <a name="best"></a> Procedure consigliate per la progettazione e l'implementazione di applicazioni  
  
-   Quando si progettano e implementano applicazioni che utilizzano FILESTREAM, tenere presenti le linee guida seguenti:  
  
-   Utilizzare NULL anziché 0x per rappresentare una colonna FILESTREAM non inizializzata. Il valore 0x provoca la creazione di un file, a differenza di NULL.  
  
-   Evitare di eseguire operazioni di inserimento ed eliminazione nelle tabelle che contengono colonne FILESTREAM non Null. Le operazioni di inserimento ed eliminazione possono modificare le tabelle FILESTREAM utilizzate per Garbage Collection. In questo caso, è possibile che le prestazioni dell'applicazione si riducano nel corso del tempo.  
  
-   Nelle applicazioni che utilizzano la replica, utilizzare NEWSEQUENTIALID() anziché NEWID(). NEWSEQUENTIALID() offre prestazioni migliori di NEWID() per la generazione dei GUID in queste applicazioni.  
  
-   L'API FILESTREAM è progettata per l'accesso ai dati tramite flusso Win32. Evitare di usare [!INCLUDE[tsql](../../includes/tsql-md.md)] per la lettura o la scrittura di oggetti BLOB di FILESTREAM di dimensioni maggiori di 2 MB. Se è necessario leggere o scrivere dati BLOB da [!INCLUDE[tsql](../../includes/tsql-md.md)], verificare che tutti i dati BLOB vengano utilizzati prima di tentare di aprire l'oggetto BLOB di FILESTREAM da Win32. Se non vengono utilizzati tutti i dati [!INCLUDE[tsql](../../includes/tsql-md.md)] , è possibile che le successive operazioni di apertura o chiusura di FILESTREAM non riescano.  
  
-   Evitare di utilizzare istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] per aggiornare, aggiungere o anteporre dati all'oggetto BLOB di FILESTREAM. In caso contrario, si verificherà lo spooling dei dati BLOB nel database tempdb e quindi in un nuovo file fisico.  
  
-   Evitare di aggiungere piccoli aggiornamenti BLOB a un oggetto BLOB di FILESTREAM. Con ogni operazione di aggiunta, vengono copiati i file FILESTREAM sottostanti. Se un'applicazione deve aggiungere piccoli oggetti BLOB, scrivere tali oggetti in una colonna **varbinary(max)** , quindi eseguire una sola operazione di scrittura nell'oggetto BLOB di FILESTREAM quando il numero di oggetti BLOB raggiunge un limite predeterminato.  
  
-   Evitare di recuperare la lunghezza dei dati di molti file BLOB in un'applicazione. Si tratta di un'operazione dispendiosa in termini di tempo perché le dimensioni non vengono archiviate nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Se è necessario determinare la lunghezza di un file BLOB, usare la funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] DATALENGTH() per determinare le dimensioni dell'oggetto BLOB, se è chiuso. DATALENGTH() non apre il file BLOB per determinarne le dimensioni.  
  
-   Se in un'applicazione viene utilizzato il protocollo Message Block1 (SMB1), i dati BLOB di FILESTREAM devono essere letti in multipli di 60 KB per ottimizzare le prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Evitare conflitti con le operazioni del database nelle applicazioni di FILESTREAM](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [Accesso ai dati FILESTREAM con OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Dati BLOB (Binary Large Object) &#40;Blob&#41; Data &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Esecuzione di aggiornamenti parziali di dati FILESTREAM](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
  
  
