---
title: Impostare il livello di compatibilità per le pubblicazioni di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], replication
- backward compatibility [SQL Server], replication
- publications [SQL Server replication], backward compatibility
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7aecff691139b1041a928c42c3df2987c992cd91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68199315"
---
# <a name="set-the-compatibility-level-for-merge-publications"></a>Impostazione del livello di compatibilità per le pubblicazioni di tipo merge
  In questo argomento si illustra come impostare il livello di compatibilità per le pubblicazioni di tipo merge in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Il livello di compatibilità delle pubblicazioni viene utilizzato nella replica di tipo merge per determinare le funzionalità che possono essere utilizzate dalle pubblicazioni in un determinato database.  
  
 **Contenuto dell'articolo**  
  
-   **Per impostare il livello di compatibilità per le pubblicazioni di tipo merge, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 Impostare il livello di compatibilità nella pagina **Tipi di Sottoscrittore** della Creazione guidata nuova pubblicazione. Per ulteriori informazioni sull'accesso a questa procedura guidata, vedere [Create a Publication](create-a-publication.md). Dopo la creazione di uno snapshot della pubblicazione, il livello di compatibilità può essere incrementato, ma non ridotto. Incrementare il livello di compatibilità nella pagina **Generale** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](view-and-modify-publication-properties.md). Incrementando il livello di compatibilità della pubblicazione, qualsiasi sottoscrizione esistente in server che eseguono versioni che risultano precedenti a tale livello di compatibilità non saranno più in grado di eseguire la sincronizzazione.  
  
> [!NOTE]  
>  Poiché il livello di compatibilità influisce su altre proprietà della pubblicazione e sugli articoli per cui tali proprietà sono valide, non modificare il livello di compatibilità e le altre proprietà in un'unica operazione all'interno della finestra di dialogo. Dopo la modifica della proprietà, lo snapshot per la pubblicazione dovrà essere rigenerato.  
  
#### <a name="to-set-the-publication-compatibility-level"></a>Per impostare il livello di compatibilità della pubblicazione  
  
-   Nella pagina **Tipi di Sottoscrittore** della Creazione guidata nuova pubblicazione selezionare i tipi di Sottoscrittori che la pubblicazione dovrà supportare.  
  
#### <a name="to-increase-the-publication-compatibility-level"></a>Per incrementare il livello di compatibilità della pubblicazione  
  
-   Nella pagina **Generale** della finestra di dialogo **Proprietà di pubblicazione - \<Pubblicazione>** selezionare il **Livello di compatibilità** desiderato.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 È possibile impostare il livello di compatibilità per una pubblicazione di tipo merge a livello di programmazione codice quando una pubblicazione viene creata o modificata a livello di programmazione in un secondo momento. Per impostare o modificare questa proprietà di pubblicazione, è possibile utilizzare le stored procedure di replica.  
  
#### <a name="to-set-the-publication-compatibility-level-for-a-merge-publication"></a>Per impostare il livello di compatibilità per una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_addmergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), specificando un valore **@publication_compatibility_level** per per rendere la pubblicazione compatibile con le versioni [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]precedenti di. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-change-the-publication-compatibility-level-of-a-merge-publication"></a>Per modificare il livello di compatibilità di una pubblicazione di tipo merge  
  
1.  Eseguire [sp_changemergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), specificando **publication_compatibility_level** per **@property** e il livello di compatibilità della **@value**pubblicazione appropriato per.  
  
#### <a name="to-determine-the-publication-compatibility-level-of-a-merge-publication"></a>Per determinare il livello di compatibilità di una pubblicazione di tipo merge  
  
1.  Eseguire [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), specificando la pubblicazione desiderata.  
  
2.  Individuare il livello di compatibilità della pubblicazione nella colonna **backward_comp_level** del set di risultati.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questo esempio viene creata una pubblicazione di tipo merge e viene impostato il livello di compatibilità della pubblicazione.  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 In questo esempio viene modificato il livello di compatibilità per la pubblicazione di tipo merge.  
  
> [!NOTE]  
>  È possibile che la modifica del livello di compatibilità della pubblicazione non sia consentita se nella pubblicazione vengono utilizzate caratteristiche che richiedono un livello di compatibilità specifico. Per altre informazioni, vedere [Compatibilità con le versioni precedenti della replica](../replication-backward-compatibility.md).  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 In questo esempio viene restituito il livello di compatibilità corrente per la pubblicazione di tipo merge.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una pubblicazione](create-a-publication.md)  
  
  
