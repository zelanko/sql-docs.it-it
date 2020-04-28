---
title: Replica in sottoscrittori di tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9f58e472b0b6e6d164e45c2d1136c81bc4a46d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68811234"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>Replica in sottoscrittori di tabelle con ottimizzazione per la memoria
  Le tabelle con funzione di sottoscrittori di replica transazionale, esclusa la replica transazionale peer-to-peer, possono essere configurate come tabelle ottimizzate per la memoria. Le altre configurazioni di replica non sono compatibili con le tabelle ottimizzate per la memoria.  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>Configurazione di una tabella ottimizzata per la memoria come sottoscrittore  
 Per configurare una tabella ottimizzata per la memoria come sottoscrittore, effettuare le operazioni seguenti.  
  
 **Creare e abilitare la pubblicazione**  
  
1.  Creazione di una pubblicazione.  
  
2.  Aggiungere articoli alla pubblicazione. Per il parametro `@upd_cmd`, utilizzare la convenzione SCALL o SQL.  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **Generare uno snapshot e adattare lo schema**  
  
1.  Creare un processo di snapshot e generare uno snapshot.  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  Passare alla cartella dello snapshot. Il percorso predefinito è "C:\Programmi\Microsoft SQL Server\MSSQL12. \<Istanza> \mssql\repldata\unc\xxx\yyyymmddhhmmss\\".  
  
3.  Individuare il **. File SCH** per la tabella e aprirlo in Management Studio. Modificare lo schema della tabella e aggiornare la stored procedure, come descritto di seguito.  
  
     Valutare gli indici definiti nel file IDX. Modificare `CREATE TABLE` per specificare gli indici, i vincoli, la chiave primaria e la sintassi ottimizzata per la memoria obbligatori. Per le tabelle ottimizzate per la memoria, le colonne di indice devono essere NOT NULL e le colonne di indice di tipi di carattere devono essere Unicode e utilizzare le regole di confronto BIN2. Vedere l'esempio riportato di seguito:  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  Quando si utilizza la convenzione SCALL per il parametro `@upd_cmd`, passare al file di schema (con estensione SCH) e modificare l'istruzione di aggiornamento della tabella in `create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]` per rimuovere le colonne di chiave primaria.  
  
     Per supportare gli aggiornamenti di chiave primaria, utilizzare una stored procedure di aggiornamento personalizzata per sostituire l'istruzione di aggiornamento della chiave primaria, come riportato di seguito:  
  
    1.  Selezionare i valori di colonna mancanti (SCALL fornisce solo la colonna interessata dall'operazione di aggiornamento).  
  
    2.  Eliminare il record esistente.  
  
    3.  Inserire un nuovo record con nuovi valori forniti, inclusa la nuova chiave primaria.  
  
     La procedura di aggiornamento originale è la seguente:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     Se la chiave primaria non deve essere mai aggiornata in un server di pubblicazione. Impostare come commento l'aggiornamento di tali colonne nella procedura di aggiornamento come segue:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     Per consentire il supporto degli aggiornamenti alla chiave primaria, modificare la procedura di aggiornamento nel modo seguente:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  Creare il database del Sottoscrittore utilizzando l'opzione **eleva per l'isolamento dello snapshot** e impostare le regole di confronto predefinite su Latin1_General_CS_AS_KS_WS in caso di utilizzo di tipi di dati carattere non Unicode.  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  Applicare lo schema al database di un Sottoscrittore e salvare lo schema per un utilizzo futuro.  
  
7.  Caricare i dati (origine) del server di pubblicazione nel sottoscrittore. I dati non devono essere modificati nel server di pubblicazione finché non si aggiunge una sottoscrizione.  È possibile utilizzare BCP come illustrato di seguito:  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  Riconfigurare l'articolo per disabilitare le modifiche dello schema nel sottoscrittore:  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **Aggiungere una sottoscrizione no sync**  
  
 Aggiungere una sottoscrizione no sync.  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 Le tabelle con ottimizzazione per la memoria dovrebbero ora iniziare a ricevere aggiornamenti dal server di pubblicazione.  
  
## <a name="restrictions"></a>Restrizioni  
 È supportata una sola replica transazionale unidirezionale. La replica transazionale peer-to-peer non è supportata.  
  
 Non è possibile pubblicare le tabelle con ottimizzazione per la memoria.  
  
 Non è possibile configurare le tabelle di replica nel distributore come tabelle ottimizzate per la memoria.  
  
 La replica di tipo merge non può includere tabelle ottimizzate per la memoria.  
  
 Nel sottoscrittore le tabelle interessate dalla replica transazionale possono essere configurate come tabelle ottimizzate per la memoria, ma le tabelle del sottoscrittore devono soddisfare i requisiti delle tabelle ottimizzate per la memoria. Si applicano pertanto le restrizioni seguenti.  
  
-   Per creare una tabella ottimizzata per la memoria in un sottoscrittore di replica transazionale, è necessario modificare manualmente i file dello schema dello snapshot utilizzati per creare le tabelle ottimizzate per la memoria. Per ulteriori informazioni, vedere [modifica di un file di schema](#Schema).  
  
-   Alle tabelle replicate in tabelle ottimizzate per la memoria in un sottoscrittore si applica il limite di 8060 byte per riga delle tabelle ottimizzate per la memoria.  
  
-   Le tabelle replicate in tabelle ottimizzate per la memoria in un sottoscrittore sono limitate ai tipi di dati consentiti nelle tabelle ottimizzate per la memoria. Per ulteriori informazioni, vedere [tipi di dati supportati](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md).  
  
-   Vengono applicate restrizioni all'aggiornamento della chiave primaria delle tabelle replicate in una tabella ottimizzata per la memoria in un sottoscrittore. Per ulteriori informazioni, vedere [replica delle modifiche in una chiave primaria](#PrimaryKey).  
  
-   Chiave esterna, vincolo univoco, trigger, modifiche dello schema, ROWGUIDCOL, colonne calcolate, compressione dei dati, tipi di dati alias, controllo delle versioni e blocchi non sono supportati nelle tabelle ottimizzate per la memoria. Per informazioni, vedere [Transact-SQL Constructs Not Supported by In-Memory OLTP](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) .  
  
##  <a name="modifying-a-schema-file"></a><a name="Schema"></a>Modifica di un file di schema  
  
-   Gli indici cluster non sono supportati. Modificare gli indici cluster in indici non cluster.  
  
-   Tutte le colonne nella chiave di un indice devono essere specificate come `NOT NULL`.  
  
-   Se si utilizza l'opzione della tabella ottimizzata per la memoria `DURABILITY = SCHEMA_AND_DATA`, la tabella deve disporre di un indice di chiave primaria non cluster.  
  
-   ANSI_PADDING deve essere ON.  
  
##  <a name="replicating-changes-to-a-primary-key"></a><a name="PrimaryKey"></a>Replica delle modifiche a una chiave primaria  
 Non è possibile aggiornare la chiave primaria di una tabella ottimizzata per la memoria. Per replicare un aggiornamento della chiave primaria in un sottoscrittore, modificare la stored procedure di aggiornamento per recapitare l'aggiornamento come coppia di eliminazione e inserimento.  
  
## <a name="see-also"></a>Vedere anche  
 [Replica SQL Server](sql-server-replication.md)  
  
  
