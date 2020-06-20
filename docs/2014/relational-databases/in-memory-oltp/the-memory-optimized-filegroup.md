---
title: Filegroup con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ffcf41775142b0347e4d05d757cdbe971791f969
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025583"
---
# <a name="the-memory-optimized-filegroup"></a>Filegroup con ottimizzazione per la memoria
  Per creare tabelle ottimizzate per la memoria, è necessario creare prima un filegroup ottimizzato per la memoria. Nel filegroup ottimizzato per la memoria è presente uno o più contenitori. Ogni contenitore include file di dati o file differenziali o entrambi.  
  
 Anche se le righe di dati delle tabelle `SCHEMA_ONLY` non sono persistenti e i metadati per le tabelle ottimizzate per la memoria e le stored procedure compilate a livello nativo vengono archiviati nei cataloghi tradizionali, il motore [!INCLUDE[hek_2](../../includes/hek-2-md.md)] richiede comunque un filegroup ottimizzato per la memoria per le tabelle ottimizzate per la memoria `SCHEMA_ONLY` per fornire un'esperienza uniforme per i database con tabelle ottimizzate per la memoria.  
  
 Il filegroup ottimizzato per la memoria è basato sul filegroup filestream, con le differenze seguenti:  
  
-   È possibile creare un solo filegroup ottimizzato per la memoria per database. È necessario contrassegnare in modo esplicito il filegroup come contenente memory_optimized_data. È possibile creare il filegroup durante la creazione del database o è possibile aggiungerlo successivamente:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   È necessario aggiungere uno o più contenitori al filegroup MEMORY_OPTIMIZED_DATA. Ad esempio:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Non è necessario abilitare il filestream ([Abilitare e configurare FILESTREAM](../blob/enable-and-configure-filestream.md)) per creare un filegroup ottimizzato per la memoria. Il mapping al filestream viene eseguito dal motore [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   È possibile aggiungere nuovi contenitori a un filegroup ottimizzato per la memoria. Potrebbe essere necessario un nuovo contenitore per espandere lo spazio di archiviazione necessario per la tabella ottimizzata per la memoria durevole e anche per distribuire I/O tra più contenitori.  
  
-   Lo spostamento di dati a un filegroup ottimizzato per la memoria è ottimizzato in una configurazione del gruppo di disponibilità AlwaysOn. Diversamente dai file filestream inviati alle repliche secondarie, i file del checkpoint (dati e differenziali) nel filegroup ottimizzato per la memoria non vengono inviati alle repliche secondarie. I file di dati e differenziali vengono costruiti utilizzando il log delle transazioni sulla replica secondaria.  
  
Di seguito sono riportate le limitazioni del filegroup ottimizzato per la memoria.  
  
-   Dopo aver creato un filegroup ottimizzato per la memoria è possibile rimuoverlo solo eliminando il database. In un ambiente di produzione, è improbabile che si renda necessario rimuovere il filegroup ottimizzato per la memoria.  
  
-   Non è possibile eliminare un contenitore non vuoto o spostare le coppie di file di dati e differenziali in un altro contenitore del filegroup ottimizzato per la memoria.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurazione di un filegroup con ottimizzazione per la memoria  
Creare più contenitori nel filegroup ottimizzato per la memoria e distribuirli in unità differenti per ottenere più larghezza di banda per trasmettere i dati in memoria.  
  
Nel configurare l'archiviazione, è necessario fornire uno spazio libero su disco quattro volte superiore alla dimensione delle tabelle ottimizzate per la memoria durevoli. Verificare che il sottosistema di I/O supporti le operazioni di IOPS necessarie per il carico di lavoro. Se le coppie di file di dati e differenziali vengono popolati in un'operazione di IOPS specifica, tale IOPS è necessaria tre volte per le operazioni di merge e archiviazione. È possibile aggiungere capacità di archiviazione e IOPS aggiungendo uno o più contenitori al filegroup ottimizzato per la memoria.  
  
In uno scenario con più contenitori e più unità, i file di dati e differenziali vengono allocati in contenitori con un meccanismo round robin. Il primo file di dati viene allocato dal primo contenitore e il file differenziale viene allocato dal contenitore successivo e questo modello di allocazione si ripete. Questo schema di allocazione distribuisce i file di dati e differenziali uniformemente nei contenitori se si dispone di un numero dispari di unità, ciascuna con il mapping a un solo contenitore. Tuttavia, se si dispone di un numero pari di unità, ciascuna con il mapping a un contenitore, è possibile che si verifichi un'archiviazione sbilanciata con i file di dati per cui è stato eseguito il mapping alle unità dispari e i file differenziali per cui è stato eseguito il mapping alle unità pari. Per ottenere un flusso di I/O bilanciato durante il ripristino, provare a inserire coppie di file di dati e differenziali sullo stesso mandrino/archiviazione come descritto nell'esempio riportato di seguito.  

> [!CAUTION]
> Se per il filegroup con ottimizzazione per la memoria è impostato un valore `MAXSIZE` e i file del checkpoint superano le dimensioni massime del contenitore, il database verrà contrassegnato come sospetto.   
> In questo caso, non provare a impostare il database come OFFLINE o ONLINE, perché il database rimarrebbe nello stato RECOVERY_PENDING.
  
### <a name="example"></a>Esempio 
Si consideri un filegroup ottimizzato per la memoria con due contenitori: il contenitore 1 sull'unità X e il contenitore 2 sulle unità Y.  
Dal momento che l'allocazione dei file di dati e differenziali viene eseguita in modo round robin, il contenitore 1 includerà solo file di dati e il contenitore 2 avrà solo file differenziali, generando una persistenza sbilanciata per l'archiviazione e le operazioni di input/output al secondo, in quanto i file di dati sono molto più grandi dei file differenziali.    
Per distribuire i file di dati e differenziali in modo uniforme tra le unità X e Y, creare quattro contenitori anziché due ed eseguire il mapping dei primi due contenitori all'unità X e dei due contenitori successivi per l'unità Y.  
Con l'allocazione round robin, i primi dati e il primo file differenziale verranno allocati rispettivamente dal contenitore-1 e dal contenitore-2, mappati all'unità X.   
Analogamente, il file di dati e differenziali successivi verrà allocato da container-3 e container-4, mappati all'unità Y. In questo modo è possibile distribuire uniformemente i file di dati e differenziali in due unità.  
 
  
## <a name="see-also"></a>Vedere anche  
[Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](creating-and-managing-storage-for-memory-optimized-objects.md)     
[Filegroup e file di database](../../relational-databases/databases/database-files-and-filegroups.md)    
  
