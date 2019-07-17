---
title: Utilizzo di un database di gestione temporanea - Parallel Data Warehouse | Microsoft Docs
description: SQL Server Parallel Data Warehouse (PDW) usa un database di gestione temporanea per archiviare i dati temporaneamente durante il processo di caricamento.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 824ad4dedee0224023f50b6855b2de1e53581304
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960039"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>Utilizzo di un database di gestione temporanea in Parallel Data Warehouse (PDW)
SQL Server Parallel Data Warehouse (PDW) usa un database di gestione temporanea per archiviare i dati temporaneamente durante il processo di caricamento. Per impostazione predefinita, SQL Server PDW Usa il database di destinazione come database di gestione temporanea, causando la frammentazione della tabella. Per ridurre la frammentazione della tabella, è possibile creare un database di gestione temporanea definita dall'utente. In alternativa, eseguire il rollback di un errore di caricamento non è un problema, è possibile usare la modalità di caricamento di fastappend per migliorare le prestazioni ignorando la tabella temporanea e caricando direttamente nella tabella di destinazione.  
  
## <a name="StagingDatabase"></a>Nozioni fondamentali sui database di gestione temporanea  
Oggetto *database di gestione temporanea* è un database PDW creati dall'utente che archivia i dati temporaneamente mentre viene caricato nell'appliance. Quando viene specificato un database di gestione temporanea per un caricamento, l'appliance copia prima di tutto i dati al database di gestione temporanea e quindi copia i dati da tabelle temporanee nel database di gestione temporanea alle tabelle permanenti nel database di destinazione.  
  
Quando un database di gestione temporanea non è specificato per un carico, ServerPDW SQL consente di creare le tabelle temporanee nel database di destinazione e li utilizza per archiviare i dati caricati prima di inserire i dati caricati nelle tabelle di destinazione permanente.  
  
Quando un carico Usa il *modalità fastappend*, SQL ServerPDW Ignora usando completamente le tabelle temporanee e aggiunge i dati direttamente alla tabella di destinazione. La modalità fastappend migliora le prestazioni di caricamento per gli scenari ELT in cui i dati vengono caricati in una tabella che rappresenta una tabella temporanea dal punto di vista dell'applicazione. Ad esempio, un processo ELT è stato possibile caricare i dati in una tabella temporanea, elaborare i dati dall'attività di pulizia e duping deprovisioning e quindi inserire i dati nella tabella dei fatti di destinazione. In questo caso, non è necessario per PDW caricare prima i dati in una tabella temporanea interna prima di inserire i dati in tabella temporanea dell'applicazione. La modalità fastappend evita il passaggio di carico aggiuntivo, che migliora significativamente le prestazioni di caricamento. Per usare la modalità fastappend, è necessario usare la modalità di transazione più, il che significa che il ripristino da un carico interrotto o non deve essere gestito dal proprio processo di caricamento.  
  
**Vantaggi di database di gestione temporanea**  
  
Il vantaggio principale di un database di gestione temporanea è per ridurre la frammentazione della tabella. Se non viene utilizzato un database di gestione temporanea, i dati vengono caricati in tabelle temporanee nel database di destinazione. Quando le tabelle temporanee ottengano vengono create ed eliminate nel database di destinazione, le pagine per le tabelle temporanee e tabelle permanenti diventano interleave. Nel corso del tempo frammentazione della tabella viene generato e comporta una riduzione delle prestazioni. Al contrario, un database di gestione temporanea assicura che le tabelle temporanee vengono create ed eliminate in uno spazio file separato rispetto a tabelle permanenti.  
  
**Strutture di tabelle di database di gestione temporanea**  
  
La struttura di archiviazione per ogni tabella di database dipende dalla tabella di destinazione.  
  
-   Per i carichi in un heap o un indice columnstore cluster, la tabella di staging è un heap.  
  
-   Per i carichi in un indice rowstore cluster, la tabella di staging è un indice rowstore cluster.  
  
## <a name="Permissions"></a>Permissions  
Richiede l'autorizzazione CREATE (per la creazione di una tabella temporanea) nel database di gestione temporanea. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>Le procedure consigliate per la creazione di un database di gestione temporanea  
  
1.  Deve essere presente solo un database di gestione temporanea per ogni dispositivo. Il database di gestione temporanea può essere condiviso da tutti i processi di caricamento per tutti i database di destinazione.  
  
2.  La dimensione del database di gestione temporanea è specifico del cliente. Inizialmente, durante il popolamento prima di tutto l'appliance, il database di gestione temporanea deve essere sufficientemente grande da contenere i processi di caricamento iniziale. Questi caricare i processi tendono a essere di grandi dimensioni perché più caricamenti possono venire generati contemporaneamente. Dopo aver completato i processi di caricamento iniziale e il sistema è in fase di produzione, sono probabile siano di dimensioni ridotte le dimensioni di ogni processo di caricamento. Quando si carica è troppo piccoli, è possibile ridurre le dimensioni del database di gestione temporanea per soddisfare il carico di dimensioni inferiori. Per ridurre le dimensioni, è possibile eliminare il database di gestione temporanea e crearla nuovamente con allocazioni di dimensioni inferiori, oppure è possibile usare la [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) istruzione.  
  
    Quando si crea il database di gestione temporanea, usare le linee guida seguenti.  
  
    -   Le dimensioni della tabella replicata devono essere la dimensione stimata, per ogni nodo di calcolo, di tutte le tabelle replicate che verranno caricati simultaneamente. La dimensione è in genere 25 a 30 GB.  
  
    -   Le dimensioni di una tabella distribuita devono essere le dimensioni stimate, per ogni dispositivo, di tutte le tabelle distribuite che verranno caricati simultaneamente.  
  
    -   Le dimensioni del log sono in genere simile a quella tabella replicata.  
  
## <a name="Examples"></a>Esempi  
  
### <a name="a-create-a-staging-database"></a>R. Creare un database di gestione temporanea 
L'esempio seguente crea un database di gestione temporanea, Stagedb, per l'utilizzo con tutti i caricamenti nell'appliance. Si supponga che si prevede che cinque replicate le tabelle delle dimensioni da 5 GB ogni caricherà contemporaneamente. Questa concorrenza comporta l'allocazione di almeno 25 GB per le dimensioni replicata. Si supponga che si stima che sei distribuito le tabelle delle dimensioni di 100, 200, 400, 500, 500 e 550 GB caricherà contemporaneamente. Questa concorrenza comporta l'allocazione di almeno 2 250 GB per le dimensioni delle tabelle distribuite.  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
