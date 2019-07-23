---
title: Supporto di SQL Server Management Studio per OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ee847b5f-6a1a-448e-a746-d61a023881ff
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 75cf54d5e52b708bf50d45ddefa7beaf1f3a8fef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086269"
---
# <a name="sql-server-management-studio-support-for-in-memory-oltp"></a>Supporto di SQL Server Management Studio per OLTP in memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è un ambiente integrato per la gestione dell'infrastruttura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornisce gli strumenti per configurare, monitorare e amministrare le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [SQL Server Management Studio](https://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b)  
  
 Nelle attività di questo argomento viene descritto come utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire le tabelle ottimizzate per la memoria, gli indici delle tabelle ottimizzate per la memoria, le stored procedure compilate in modo nativo, i tipi di tabella ottimizzata per la memoria definiti dall'utente.  
  
 Per informazioni su come creare tabelle ottimizzate per la memoria a livello di codice, vedere [Creazione di una tabella ottimizzata per la memoria e di una stored procedure compilata in modo nativo](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
### <a name="to-create-a-database-with-a-memory-optimized-data-filegroup"></a>Per creare un database con un filegroup di dati ottimizzato per la memoria  
  
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed espanderla.  
  
2.  Fare clic con il pulsante destro del mouse su **Database**, quindi scegliere **Nuovo database**.  
  
3.  Per aggiungere un nuovo filegroup di dati ottimizzato per la memoria, fare clic sulla pagina **Filegroup**. In **DATI OTTIMIZZATI PER LA MEMORIA** fare clic su **Aggiungi filegroup**, quindi immettere il nome del filegroup di dati ottimizzato per la memoria.  La colonna con etichetta **File FILESTREAM** rappresenta il numero di contenitori del filegroup. I contenitori vengono aggiunti alla pagina **Generale** .  
  
4.  Per aggiungere un file (contenitore) a un filegroup, fare clic sulla pagina **Generale** . In **File di database**fare clic su **Aggiungi**. Selezionare **Tipo file** come **Dati FILESTREAM**, specificare il nome logico del contenitore, selezionare il filegroup ottimizzato per la memoria e verificare che **Aumento automatico / Dimensioni max** sia impostato su **Senza limiti**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     For more information on how to create a new database by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], see [Create a Database](../../relational-databases/databases/create-a-database.md).  
  
### <a name="to-create-a-memory-optimized-table"></a>Per creare una tabella ottimizzata per la memoria  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sul nodo **Tabelle** del database, scegliere **Nuova**, quindi fare clic su **Tabella con ottimizzazione per la memoria**.  
  
     Verrà visualizzato un modello per creare tabelle ottimizzate per la memoria.  
  
2.  Per sostituire i parametri del modello, scegliere **Imposta valori per parametri modello** dal menu **Query** .  
  
     Per altre informazioni sulla modalità d'uso dei modelli, vedere [Esplora modelli](../../ssms/template/template-explorer.md).  
  
3.  In **Esplora oggetti** le tabelle vengono ordinate prima in base alle tabelle basate su disco e quindi in base alle tabelle ottimizzate per la memoria. Usare **Dettagli Esplora oggetti** per visualizzare tutte le tabelle ordinate in base al nome.  
  
### <a name="to-create-a-natively-compiled-stored-procedure"></a>Per creare una stored procedure compilata in modo nativo  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sul nodo **Stored procedure** del database, scegliere **Nuova**, quindi fare clic su **Stored procedure compilata in modo nativo**.  
  
     Verrà visualizzato un modello per la creazione di stored procedure compilate in modo nativo.  
  
2.  Per sostituire i parametri del modello, scegliere **Imposta valori per parametri modello** dal menu **Query**.  
  
     Per altre informazioni sulla creazione di nuove stored procedure, vedere [Creazione di una stored procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md).  
  
### <a name="to-create-a-user-defined-memory-optimized-table-type"></a>Per creare una tipo di tabella ottimizzata per la memoria definito dall'utente  
  
1.  In **Esplora oggetti**espandere il nodo **Tipi** del database, fare clic con il pulsante destro del mouse sul nodo **Tipi di tabella definiti dall'utente** , fare clic su **Nuova**, quindi scegliere **Tipo di tabella con ottimizzazione per la memoria definito dall'utente**.  
  
     Viene visualizzato un modello per la creazione di un tipo di tabella ottimizzata per la memoria definito dall'utente.  
  
2.  Per sostituire i parametri del modello, scegliere **Imposta valori per parametri modello** dal menu **Query**.  
  
     Per altre informazioni sulla creazione di nuove stored procedure, vedere [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
## <a name="memory-monitoring"></a>Monitoraggio della memoria  
  
#### <a name="view-memory-usage-by-memory-optimized-objects-report"></a>Visualizzare l'utilizzo della memoria con il report relativo agli oggetti con ottimizzazione per la memoria  
  
-   In **Esplora oggetti**fare clic con il pulsante destro del mouse sul database, scegliere **Report**, fare clic su **Report standard**, quindi su **Utilizzo memoria da oggetti con ottimizzazione per la memoria**.  
  
     Questo report include informazioni dettagliate sull'utilizzo dello spazio in memoria da parte di oggetti ottimizzati per la memoria nel database.  
  
#### <a name="view-properties-for-allocated-and-used-memory-for-a-table-database"></a>Visualizzazione delle proprietà relative alla memoria allocata e utilizzata per una tabella o un database  
  
1.  Per ottenere informazioni sull'utilizzo in memoria:  
  
    -   In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella ottimizzata per la memoria, scegliere **Proprietà**, quindi la pagina **Archiviazione**. Il valore della proprietà **Spazio dati** indica la memoria usata dai dati nella tabella. Il valore della proprietà **Spazio degli indici** indica la memoria usata dagli indici nella tabella.  
  
    -   In **Esplora oggetti**fare clic con il pulsante destro del mouse sul database, scegliere **Proprietà**, quindi fare clic sulla pagina **Generale** . Il valore della proprietà **Memoria allocata agli oggetti ottimizzati in memoria** indica la memoria allocata agli oggetti ottimizzati per la memoria nel database. Il valore della proprietà **Memoria utilizzata dagli oggetti ottimizzati in memoria** indica la memoria usata dagli oggetti ottimizzati per la memoria nel database.  
  
## <a name="supported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>Funzionalità supportate in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] supporta le funzionalità e le operazioni supportate dal motore di database nei database con filegroup di dati ottimizzati per la memoria, tabelle ottimizzate per la memoria, indici e stored procedure compilate in modo nativo.  
  
 Per gli oggetti di database, tabella, stored procedure, tipo di tabella definito dall'utente o indice, le seguenti funzionalità di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono state aggiornate o estese per supportare OLTP in memoria.  
  
-   Esplora oggetti  
  
    -   Menu di scelta rapida  
  
    -   Impostazioni filtro  
  
    -   Salva script con nome  
  
    -   Attività  
  
    -   Report  
  
    -   Proprietà  
  
    -   Attività per i database:  
  
        -   Collegamento e scollegamento di un database contenente tabelle ottimizzate per la memoria.  
  
             Nell'interfaccia utente **Collega database** non è visualizzato il filegroup di dati ottimizzato per la memoria. È tuttavia possibile proseguire con l'operazione di collegamento del database e il database verrà collegato correttamente.  
  
            > [!NOTE]  
            >  Se si desidera utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per collegare un database che dispone di un contenitore di filegroup di dati ottimizzati per la memoria e questo contenitore è stato creato anche in un altro computer, il percorso del contenitore di filegroup di dati ottimizzati per la memoria deve essere lo stesso per entrambi i computer. Se si desidera che il percorso del contenitore del filegroup di dati ottimizzati per la memoria per la memoria sia diverso nel nuovo computer, è possibile utilizzare [!INCLUDE[tsql](../../includes/tsql-md.md)] per collegare il database. Nell'esempio seguente il percorso del contenitore del filegroup di dati ottimizzato per la memoria nel nuovo computer è C:\Folder2, ma al momento della creazione del contenitore del filegroup di dati, il percorso nel primo computer era C:\Folder1.  
            >   
            >  `CREATE DATABASE[imoltp] ON`  
            >   
            >  `(NAME =N'imoltp',FILENAME=N'C:\Folder2\imoltp.mdf'),`  
            >   
            >  `(NAME =N'imoltp_mod1',FILENAME=N'C:\Folder2\imoltp_mod1'),`  
            >   
            >  `(NAME =N'imoltp_log',FILENAME=N'C:\Folder2\imoltp_log.ldf')`  
            >   
            >  `FOR ATTACH`  
            >   
            >  `GO`  
  
        -   Generare script.  
  
             In **Procedura guidata Genera e pubblica script** il valore predefinito per l'opzione di scripting **Verifica esistenza oggetto** è FALSE. Se il valore dell'opzione di scripting **Verifica esistenza oggetto** è impostato su TRUE nella schermata **Imposta opzioni di generazione script** della procedura guidata, lo script generato contiene "CREATE PROCEDURE <nome_procedura> AS" e "ALTER PROCEDURE <nome_procedura> <definizione_procedura>". Quando viene eseguito, lo script generato restituisce un errore perché l'istruzione ALTER PROCEDURE non è supportata nelle stored procedure compilate in modo nativo.  
  
             Per modificare lo script generato per ogni stored procedure compilata in modo nativo:  
  
            1.  In "CREATE PROCEDURE <procedure_name> AS", sostituire "AS" con "<procedure_definition>".  
  
            2.  Eliminare "ALTER PROCEDURE <procedure_name> <procedure_definition>".  
  
        -   Copiare database. Per i database con oggetti ottimizzati per la memoria, la creazione del database nel server di destinazione e il trasferimento dei dati non verranno eseguiti in una transazione.  
  
        -   Importare ed esportare dati. Usare l'opzione **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Copia i dati da una o più tabelle o viste dell'Importazione/Esportazione guidata** . Se la tabella di destinazione è una tabella ottimizzata per la memoria non presente nel database di destinazione:  
  
            1.  Nella schermata **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Impostazione copia tabella o query**dell' **Importazione/esportazione guidata** selezionare **Copia i dati da una o più tabelle o viste**. Fare quindi clic su **Avanti**.  
  
            2.  Fare clic su **Modifica mapping**. Selezionare quindi **Crea tabella di destinazione** e fare clic su **Modifica SQL**. Immettere la sintassi CREATE TABLE per creare una tabella ottimizzata per la memoria nel database di destinazione. Fare clic su **OK** e completare i passaggi rimanenti della procedura guidata.  
  
        -   Piani di manutenzione. Le attività di manutenzione Riorganizza indice e Ricompila indice non sono supportate nelle tabelle ottimizzate per la memoria e nei relativi indici. Pertanto, quando viene eseguito un piano di manutenzione per la ricompilazione e la riorganizzazione dell'indice, le tabelle ottimizzate per la memoria e i relativi indici nei database selezionati vengono omessi.  
  
             L'aggiornamento delle statistiche delle attività di manutenzione non è supportato con un'analisi di esempio nelle tabelle ottimizzate per la memoria e i relativi indici. Pertanto, quando viene eseguito un piano di manutenzione per l'aggiornamento delle statistiche, le statistiche per le tabelle ottimizzate per la memoria e i relativi indici vengono aggiornate sempre a **WITH FULLSCAN, NORECOMPUTE**.  
  
-   Riquadro Dettagli di Esplora oggetti  
  
-   Esplora modelli  
  
## <a name="unsupported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>Funzionalità non supportate in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 Per gli oggetti di OLTP in memoria, in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] non sono supportate funzionalità e operazioni non supportate anche dal motore di database.  
  
 Per altre informazioni sulla funzionalitè di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supportate, vedere [Funzionalità di SQL Server non supportate per OLTP in memoria](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di SQL Server per OLTP in memoria](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  
