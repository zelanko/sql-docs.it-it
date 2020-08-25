---
title: Utilizzo di un database di gestione temporanea
description: SQL Server Parallel data warehouse (PDW) utilizza un database di gestione temporanea per archiviare temporaneamente i dati durante il processo di caricamento.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400286"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>Uso di un database di gestione temporanea in Parallel data warehouse (PDW)
SQL Server Parallel data warehouse (PDW) utilizza un database di gestione temporanea per archiviare temporaneamente i dati durante il processo di caricamento. Per impostazione predefinita, SQL Server PDW utilizza il database di destinazione come database di gestione temporanea, che può causare la frammentazione della tabella. Per ridurre la frammentazione della tabella, è possibile creare un database di gestione temporanea definito dall'utente. In alternativa, quando il rollback da un errore di caricamento non è un problema, è possibile usare la modalità di caricamento FastAppend per migliorare le prestazioni ignorando la tabella temporanea e caricando direttamente nella tabella di destinazione.  
  
## <a name="staging-database-basics"></a><a name="StagingDatabase"></a>Nozioni fondamentali sul database di gestione temporanea  
Un *database di gestione temporanea* è un database PDW creato dall'utente che archivia i dati temporaneamente mentre viene caricato nell'appliance. Quando si specifica un database di gestione temporanea per un carico, l'appliance copia prima i dati nel database di gestione temporanea e quindi copia i dati dalle tabelle temporanee del database di gestione temporanea a tabelle permanenti nel database di destinazione.  
  
Quando un database di gestione temporanea non viene specificato per un carico, SQL ServerPDW crea le tabelle temporanee nel database di destinazione e le utilizza per archiviare i dati caricati prima di inserire i dati caricati nelle tabelle di destinazione permanenti.  
  
Quando un carico usa la *modalità FastAppend*, SQL ServerPDW ignora completamente le tabelle temporanee e aggiunge i dati direttamente alla tabella di destinazione. La modalità FastAppend migliora le prestazioni di carico per gli scenari ELT in cui i dati vengono caricati in una tabella che rappresenta una tabella temporanea dal punto di vista dell'applicazione. Un processo ELT, ad esempio, può caricare i dati in una tabella temporanea, elaborare i dati mediante pulizia e deingannarezione, quindi inserire i dati nella tabella dei fatti di destinazione. In questo caso, non è necessario che PDW carichi innanzitutto i dati in una tabella temporanea interna prima di inserire i dati nella tabella temporanea dell'applicazione. La modalità FastAppend evita il passaggio del carico aggiuntivo, che migliora significativamente le prestazioni di caricamento. Per utilizzare la modalità FastAppend, è necessario utilizzare la modalità a più transazioni, il che significa che il ripristino da un carico fallito o interrotto deve essere gestito dal proprio processo di caricamento.  
  
**Vantaggi del database di gestione temporanea**  
  
Il vantaggio principale di un database di gestione temporanea è la riduzione della frammentazione della tabella. Se non viene utilizzato un database di staging, i dati vengono caricati nelle tabelle temporanee del database di destinazione. Quando le tabelle temporanee vengono create e rilasciate nel database di destinazione, le pagine per le tabelle temporanee e le tabelle permanenti diventano Interleaved. Nel corso del tempo, la frammentazione della tabella si verifica e peggiora le prestazioni. Al contrario, un database di gestione temporanea garantisce che le tabelle temporanee vengano create ed eliminate in uno spazio file separato rispetto alle tabelle permanenti.  
  
**Strutture della tabella di database di staging**  
  
La struttura di archiviazione per ogni tabella di database dipende dalla tabella di destinazione.  
  
-   Per i caricamenti in un heap o in un indice columnstore cluster, la tabella di staging è un heap.  
  
-   Per i caricamenti in un indice cluster rowstore, la tabella di staging è un indice cluster rowstore.  
  
## <a name="permissions"></a><a name="Permissions"></a>Autorizzazioni  
È richiesta l'autorizzazione CREATE (per la creazione di una tabella temporanea) nel database di gestione temporanea. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="best-practices-for-creating-a-staging-database"></a><a name="CreatingStagingDatabase"></a>Procedure consigliate per la creazione di un database di gestione temporanea  
  
1.  Deve essere presente un solo database di gestione temporanea per ogni appliance. Il database di staging può essere condiviso da tutti i processi di caricamento per tutti i database di destinazione.  
  
2.  Le dimensioni del database di gestione temporanea sono specifiche del cliente. Inizialmente, quando si popola il dispositivo per la prima volta, il database di gestione temporanea deve essere sufficientemente grande da contenere i processi di caricamento iniziali. Questi processi di caricamento tendono a essere di grandi dimensioni in quanto possono verificarsi più caricamenti simultaneamente. Una volta completati i processi di caricamento iniziale e il sistema è in produzione, è probabile che le dimensioni di ogni processo di caricamento siano inferiori. Quando i caricamenti sono di dimensioni ridotte, è possibile ridurre le dimensioni del database di gestione temporanea per adattarle alle dimensioni di carico più ridotte. Per ridurre le dimensioni, è possibile eliminare il database di gestione temporanea e crearlo nuovamente con allocazioni di dimensioni inferiori oppure è possibile utilizzare l'istruzione [ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) .  
  
    Quando si crea il database di gestione temporanea, attenersi alle linee guida seguenti.  
  
    -   Le dimensioni della tabella replicata devono corrispondere alle dimensioni stimate, per ogni nodo di calcolo, di tutte le tabelle replicate che verranno caricate simultaneamente. La dimensione è in genere di 25-30 GB.  
  
    -   Le dimensioni della tabella distribuita devono corrispondere alle dimensioni stimate, per Appliance, di tutte le tabelle distribuite che verranno caricate simultaneamente.  
  
    -   Le dimensioni del log sono in genere simili a quelle della tabella replicata.  
  
## <a name="examples"></a><a name="Examples"></a>Esempi  
  
### <a name="a-create-a-staging-database"></a>R. Creazione di un database di gestione temporanea 
Nell'esempio seguente viene creato un database di gestione temporanea, Stagedb, da usare con tutti i carichi nell'appliance. Si supponga di stimare che cinque tabelle replicate di dimensioni pari a 5 GB vengano caricate simultaneamente. Questa concorrenza comporta l'allocazione di almeno 25 GB per la dimensione replicata. Si supponga di stimare che vengano caricate simultaneamente sei tabelle distribuite di dimensioni 100, 200, 400, 500, 500 e 550 GB. Questa concorrenza comporta l'allocazione di almeno 2250 GB per le dimensioni della tabella distribuita.  
  
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
  
