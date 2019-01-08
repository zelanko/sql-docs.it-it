---
title: Creare uno snapshot del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], creating
ms.assetid: 187fbba3-c555-4030-9bdf-0f01994c5230
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f577f7798da2ba7b7ee4259ecc98994f713cfc5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52768333"
---
# <a name="create-a-database-snapshot-transact-sql"></a>Creare uno snapshot del database (Transact-SQL)
  L'unico modo per creare uno snapshot del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] non supporta la creazione di snapshot del database.  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
     [Procedura consigliata: Denominazione degli snapshot del Database](#Naming)  
  
-   **Per creare un snapshot del database utilizzando:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Il database di origine, in cui può essere utilizzato qualsiasi modello di recupero, deve soddisfare i prerequisiti seguenti:  
  
-   L'istanza del server deve essere in esecuzione in un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che supporta gli snapshot del database. Per informazioni sul supporto per gli snapshot del database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Il database di origine deve essere online, a meno che non si tratti di un database mirror nell'ambito di una sessione di mirroring del database.  
  
-   Per creare uno snapshot del database in un database mirror, è necessario che il database si trovi nello[stato di mirroring](../../database-engine/database-mirroring/mirroring-states-sql-server.md)sincronizzato.  
  
-   Non è possibile configurare il database di origine come un database condiviso scalabile.  
  
> [!IMPORTANT]  
>  Per informazioni relative ad altre considerazioni rilevanti, vedere [Snapshot del database &#40;SQL Server&#41;](database-snapshots-sql-server.md).  
  
###  <a name="Recommendations"></a> Indicazioni  
 In questa sezione vengono illustrate le procedure consigliate seguenti:  
  
-   [Procedura consigliata: Denominazione degli snapshot del Database](#Naming)  
  
-   [Procedura consigliata: Limitazione del numero di snapshot del Database](#Limiting_Number)  
  
-   [Procedura consigliata: Connessioni client a uno Snapshot del Database](#Client_Connections)  
  
####  <a name="Naming"></a> Procedura consigliata: Denominazione degli snapshot del database  
 Prima di creare gli snapshot è importante considerare il nome da utilizzare. Ogni snapshot del database richiede un nome di database univoco. Per semplificare l'amministrazione, il nome di uno snapshot può contenere informazioni utili a identificare il database, ad esempio:  
  
-   Nome del database di origine.  
  
-   Indicazione che si tratta di uno snapshot.  
  
-   Data e ora di creazione dello snapshot, un numero di sequenza o altre informazioni utili a distinguere gli snapshot sequenziali su un determinato database.  
  
 Si consideri ad esempio una serie di snapshot del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Ogni giorno fra le 6 e le 18 vengono creati tre snapshot, a intervalli di 6 ore, su un ciclo di 24 ore. Ogni snapshot viene mantenuto per 24 ore prima di essere eliminato e sostituito da un nuovo snapshot con lo stesso nome. Si noti che il nome di ogni snapshot indica l'ora, ma non il giorno:  
  
```  
AdventureWorks_snapshot_0600  
AdventureWorks_snapshot_1200  
AdventureWorks_snapshot_1800  
```  
  
 In alternativa, se l'orario di creazione di questi snapshot giornalieri cambia da un giorno all'altro, può essere preferibile una convenzione di denominazione più generica, ad esempio:  
  
```  
AdventureWorks_snapshot_morning  
AdventureWorks_snapshot_noon  
AdventureWorks_snapshot_evening  
```  
  
####  <a name="Limiting_Number"></a> Procedura consigliata: Limitazione del numero di snapshot del database  
 Creando una serie di snapshot a intervalli di tempo si acquisiscono snapshot sequenziali del database di origine. Ogni snapshot viene mantenuto finché non viene esplicitamente eliminato. Poiché ogni snapshot continua a crescere man mano che le pagine originali vengono aggiornate, per conservare spazio su disco è consigliabile eliminare un vecchio snapshot prima di crearne uno nuovo.  
  
> [!NOTE]  
>  Se si desidera ripristinare uno snapshot del database è necessario eliminare tutti gli altri snapshot dal database.  
  
####  <a name="Client_Connections"></a> Procedura consigliata: Connessioni client a uno snapshot del database  
 Per utilizzare uno snapshot del database, i client devono sapere dove reperirlo. Gli utenti possono leggere da uno snapshot del database durante la creazione o l'eliminazione di un altro snapshot. Quando si sostituisce uno snapshot esistente con un nuovo snapshot, tuttavia, è necessario reindirizzare i client al nuovo snapshot. Gli utenti possono connettersi manualmente a uno snapshot del database tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per supportare un ambiente di produzione, è tuttavia consigliabile creare una soluzione a livello di programmazione che indirizzi in modo trasparente i client che scrivono report all'ultimo snapshot del database.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Se un utente può creare un database, può creare anche uno snapshot del database; tuttavia, per creare uno snapshot di un database mirror, è necessario essere membro del ruolo del server predefinito **sysadmin** .  
  
##  <a name="TsqlProcedure"></a> Come creare uno snapshot del database utilizzando Transact-SQL  
 **Per creare uno snapshot del database**  
  
> [!NOTE]  
>  Per un esempio di questa procedura, vedere [Esempi (Transact-SQL)](#TsqlExample)più avanti in questa sezione.  
  
1.  In base alla dimensione attuale del database di origine, assicurarsi che lo spazio su disco sia sufficiente per lo snapshot del database. La dimensione massima di uno snapshot del database corrisponde alla dimensione del database di origine al momento della creazione dello snapshot. Per altre informazioni, vedere [Visualizzare le dimensioni del file sparse di uno snapshot del database &#40;Transact-SQL&#41;](view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md).  
  
2.  Generare un'istruzione CREATE DATABASE sui file che utilizzano la clausola AS SNAPSHOT OF. Per creare uno snapshot, è necessario specificare il nome logico di ogni file di database del database di origine. La sintassi è la seguente:  
  
     CREATE DATABASE *database_snapshot_name*  
  
     ON  
  
     (  
  
     NAME =*logical_file_name*,  
  
     FILENAME ='*os_file_name*'  
  
     ) [ ,...*n* ]  
  
     AS SNAPSHOT OF *source_database_name*  
  
     [;]  
  
     Dove *source_**database_name* è il database di origine, *logical_file_name* è il nome logico usato in SQL Server quando si fa riferimento al file, *os_file_name* rappresenta il nome e il percorso usati dal sistema operativo quando si crea il file e *database_snapshot_name* è il nome dello snapshot in base a cui si vuole ripristinare il database. Per una descrizione completa di questa sintassi, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
    > [!NOTE]  
    >  Quando si crea uno snapshot del database, i file di log, i file offline, i file in fase di ripristino e i file inattivi non sono consentiti nell'istruzione CREATE DATABASE.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
  
> [!NOTE]  
>  L'estensione `.ss` utilizzata negli esempi è arbitraria.  
  
 In questa sezione sono disponibili gli esempi seguenti:  
  
-   A. [Creazione di uno snapshot del database AdventureWorks](#Creating_on_AW)  
  
-   b. [Creazione di uno snapshot del database Sales](#Creating_on_Sales)  
  
####  <a name="Creating_on_AW"></a> A. Creazione di uno snapshot del database AdventureWorks  
 In questo esempio viene creato uno snapshot del database `AdventureWorks` . Il nome dello snapshot, `AdventureWorks_dbss_1800`, e il nome del file sparse corrispondente, `AdventureWorks_data_1800.ss`, indicano l'ora di creazione, ovvero le 18.00 (1800).  
  
```  
CREATE DATABASE AdventureWorks_dbss1800 ON  
( NAME = AdventureWorks_Data, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\AdventureWorks_data_1800.ss' )  
AS SNAPSHOT OF AdventureWorks;  
GO  
```  
  
####  <a name="Creating_on_Sales"></a> B. Creazione di uno snapshot del database Sales  
 In questo esempio viene creato uno snapshot, `sales_snapshot1200`, del database `Sales` . Questo database è stato creato nell'esempio, "Creazione di un database con filegroup" nella [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
```  
--Creating sales_snapshot1200 as snapshot of the  
--Sales database:  
CREATE DATABASE sales_snapshot1200 ON  
( NAME = SPri1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SPri1dat_1200.ss'),  
( NAME = SPri2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SPri2dt_1200.ss'),  
( NAME = SGrp1Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\mssql\data\SG1Fi1dt_1200.ss'),  
( NAME = SGrp1Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG1Fi2dt_1200.ss'),  
( NAME = SGrp2Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG2Fi1dt_1200.ss'),  
( NAME = SGrp2Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG2Fi2dt_1200.ss')  
AS SNAPSHOT OF Sales;  
GO  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Visualizzazione di uno snapshot del database &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [Ripristinare un database a uno snapshot del database](revert-a-database-to-a-database-snapshot.md)  
  
-   [Eliminare uno snapshot del database &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Snapshot del database &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
