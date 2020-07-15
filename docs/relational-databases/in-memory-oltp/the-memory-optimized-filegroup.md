---
title: Filegroup con ottimizzazione per la memoria | Microsoft Docs
description: Informazioni su come creare un gruppo di file ottimizzato per la memoria, che include contenitori per i file di dati e i file differenziali, prima di creare tabelle ottimizzate per la memoria in SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 636bc0ebcfbd85f9da38ecff6cd1ff4a966164c8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715348"
---
# <a name="the-memory-optimized-filegroup"></a>Filegroup con ottimizzazione per la memoria
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Per creare tabelle ottimizzate per la memoria, è necessario creare prima un filegroup ottimizzato per la memoria. Nel filegroup ottimizzato per la memoria è presente uno o più contenitori. Ogni contenitore include file di dati o file differenziali o entrambi.  
  
 Anche se le righe di dati delle tabelle `SCHEMA_ONLY` non sono persistenti e i metadati per le tabelle ottimizzate per la memoria e le stored procedure compilate a livello nativo vengono archiviati nei cataloghi tradizionali, il motore [!INCLUDE[hek_2](../../includes/hek-2-md.md)] richiede comunque un filegroup ottimizzato per la memoria per le tabelle ottimizzate per la memoria `SCHEMA_ONLY` per fornire un'esperienza uniforme per i database con tabelle ottimizzate per la memoria.  
  
 Il filegroup ottimizzato per la memoria è basato sul filegroup filestream, con le differenze seguenti:  
  
-   È possibile creare un solo filegroup ottimizzato per la memoria per database. È necessario contrassegnare in modo esplicito il filegroup come contenente memory_optimized_data. È possibile creare il filegroup durante la creazione del database o è possibile aggiungerlo successivamente:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   È necessario aggiungere uno o più contenitori al filegroup `MEMORY_OPTIMIZED_DATA`. Ad esempio:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Non è necessario abilitare il filestream ([Abilitare e configurare FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)) per creare un filegroup ottimizzato per la memoria. Il mapping al filestream viene eseguito dal motore [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   È possibile aggiungere nuovi contenitori a un filegroup ottimizzato per la memoria. Potrebbe essere necessario un nuovo contenitore per espandere l'archiviazione necessaria per la tabella ottimizzata per la memoria durevole nonché per distribuire i dati IO tra più contenitori.  
  
-   Lo spostamento di dati a un filegroup ottimizzato per la memoria è ottimizzato in una configurazione del gruppo di disponibilità AlwaysOn. Diversamente dai file filestream inviati alle repliche secondarie, i file del checkpoint (dati e differenziali) nel filegroup ottimizzato per la memoria non vengono inviati alle repliche secondarie. I file di dati e differenziali vengono costruiti utilizzando il log delle transazioni sulla replica secondaria.  
  
Di seguito sono riportate le limitazioni da applicare al filegroup ottimizzato per la memoria:  
  
-   Dopo aver usato un filegroup ottimizzato per la memoria è possibile rimuoverlo solo eliminando il database. In un ambiente di produzione, è improbabile che si renda necessario rimuovere il filegroup ottimizzato per la memoria.  
  
-   Non è possibile eliminare un contenitore non vuoto o spostare le coppie di file di dati e differenziali in un altro contenitore del filegroup ottimizzato per la memoria.    
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurazione di un filegroup con ottimizzazione per la memoria  
Creare più contenitori nel filegroup ottimizzato per la memoria e distribuirli in unità differenti per ottenere più larghezza di banda per trasmettere i dati in memoria. 
 
In uno scenario con più contenitori e più unità, i file di dati e differenziali vengono allocati in contenitori con un meccanismo round robin. Il primo file di dati viene allocato dal primo contenitore e il file differenziale viene allocato dal contenitore successivo e questo modello di allocazione si ripete. Questo schema di allocazione distribuisce i file di dati e differenziali uniformemente nei contenitori se si dispone di un numero dispari di unità, ciascuna con il mapping a un solo contenitore. Tuttavia, se si dispone di un numero pari di unità, ciascuna con il mapping a un contenitore, è possibile che si verifichi un'archiviazione sbilanciata con i file di dati per cui è stato eseguito il mapping alle unità dispari e i file differenziali per cui è stato eseguito il mapping alle unità pari. Per ottenere un flusso bilanciato di I/O per il recupero, inserire coppie di file di dati e differenziali negli stessi spindle/archiviazione.
  
Nel configurare l'archiviazione, è necessario fornire uno spazio libero su disco quattro volte superiore alla dimensione delle tabelle ottimizzate per la memoria durevoli. Verificare, inoltre, che il sottosistema di I/O supporti le operazioni di I/O al secondo necessarie per il carico di lavoro. Se le coppie di file di dati e differenziali vengono popolati in un'operazione di IOPS specifica, tale IOPS è necessaria tre volte per le operazioni di merge e archiviazione. È possibile aggiungere capacità di archiviazione e IOPS aggiungendo uno o più contenitori al filegroup ottimizzato per la memoria.  
 
> [!CAUTION]
> Se per il filegroup con ottimizzazione per la memoria è impostato un valore `MAXSIZE` e i file del checkpoint superano le dimensioni massime del contenitore, il database verrà contrassegnato come sospetto.   
> In questo caso, non provare a impostare il database come OFFLINE o ONLINE, perché il database rimarrebbe nello stato RECOVERY_PENDING.
  
## <a name="see-also"></a>Vedere anche  
[Creazione e gestione dell'archiviazione per gli oggetti ottimizzati per la memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[Opzioni per file e filegroup ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 

