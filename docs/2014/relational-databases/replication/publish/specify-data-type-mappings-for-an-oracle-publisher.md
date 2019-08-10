---
title: Specificare i mapping tra i tipi di dati di un server di pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99e1d3377cb5ed4afd4577462e0b436bb16d2fee
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941095"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Specifica dei mapping tra i tipi di dati di un server di pubblicazione Oracle
  In questo argomento viene descritto come specificare i mapping dei tipi di dati per un server di pubblicazione Oracle in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Anche se per i server di pubblicazione Oracle è disponibile un set di mapping predefiniti di tipi di dati, può essere necessario specificare mapping diversi per una determinata pubblicazione.  
  
 **Contenuto dell'argomento**  
  
-   **Per specificare i mapping dei tipi di dati per un server di pubblicazione Oracle, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Nella scheda **Mapping dei dati** della finestra di dialogo **Proprietà articolo - \<Articolo>** specificare i mapping tra i tipi di dati. È possibile accedere a questa finestra nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione da un database Oracle](create-a-publication-from-an-oracle-database.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-data-type-mapping"></a>Per specificare un mapping tra i tipi di dati  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare una tabella e quindi fare clic su **Proprietà articolo**.  
  
2.  Fare clic su **Imposta proprietà dell'articolo tabella evidenziato**.  
  
3.  Nella scheda **Mapping dei dati** della finestra di dialogo **Proprietà articolo - \<Articolo>** , selezionare i mapping nella colonna **Tipo di dati del Sottoscrittore**:  
  
    -   Per alcuni tipi di dati è disponibile un solo tipo di mapping. In questo caso, la colonna nella proprietà è di sola lettura.  
  
    -   Per alcuni tipi è possibile selezionare più tipi di mapping. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] consiglia di utilizzare il mapping predefinito, a meno che l'applicazione utilizzata non richieda un tipo di mapping diverso. Per altre informazioni, vedere [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile specificare mapping personalizzati di tipi di dati a livello di programmazione tramite le stored procedure di replica. È inoltre possibile impostare i mapping predefiniti usati per il mapping dei tipi di dati tra un sistema di gestione di database (DBMS) [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e non-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Per definire mapping personalizzati di tipi di dati durante la creazione di un articolo appartenente a una pubblicazione Oracle  
  
1.  Se non esiste già, creare una pubblicazione Oracle.  
  
2.  Nel database di distribuzione eseguire [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Specificare il valore **0** per **\@use_default_datatypes**. Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
3.  Nel server di distribuzione eseguire [sp_helparticlecolumns](/sql/relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql) per visualizzare il mapping esistente per una colonna in un articolo pubblicato.  
  
4.  Nel server di distribuzione eseguire [sp_changearticlecolumndatatype](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql). Specificare il nome del server di pubblicazione Oracle per **\@publisher**, nonché **\@publication**, **\@article** e **\@column** per definire la colonna pubblicata. Specificare il nome del tipo di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di cui eseguire il mapping per **\@type**, nonché **\@length**, **\@precision** e **\@scale** se applicabile.  
  
5.  Nel server di distribuzione eseguire [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). In questo modo verrà creata la vista utilizzata per generare lo snapshot dalla pubblicazione Oracle.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>Per specificare un mapping come mapping predefinito per un tipo di dati  
  
1.  (Facoltativo) In un database del server di distribuzione eseguire [sp_getdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql). Specificare **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_version** e qualsiasi altro parametro necessario per identificare il sistema DBMS di origine. Le informazioni sui tipi di dati attualmente sottoposti a mapping nel sistema DBMS di destinazione vengono restituite tramite parametri di output.  
  
2.  (Facoltativo) In un database del server di distribuzione eseguire [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql). Specificare **\@source_dbms** e qualsiasi altro parametro necessario per filtrare il set di risultati. Si noti il valore di **mapping_id** per il mapping desiderato nel set di risultati.  
  
3.  In un database del database di distribuzione eseguire [sp_setdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql).  
  
    -   Se si conosce il valore desiderato di **mapping_id** ottenuto nel passaggio 2, specificarlo per **\@mapping_id**.  
  
    -   Se non si conosce il valore di **mapping_id**, specificare i parametri **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_type** e qualsiasi altro parametro necessario per identificare un mapping esistente.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>Per trovare tipi di dati validi per un determinato tipo di dati Oracle  
  
1.  In un database del server di distribuzione eseguire [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql). Specificare il valore **ORACLE** per **\@source_dbms** e qualsiasi altro parametro necessario per filtrare il set di risultati.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questo esempio viene modificata una colonna con un tipo di dati NUMBER di Oracle in modo che venga eseguito il mapping al tipo di dati `numeric` (38,38) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anziché al tipo di dati predefinito `float`.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_changecolumndatatype)]  
  
 In questo esempio di query vengono restituiti i mapping predefiniti e alternativi per il tipo di dati `CHAR` di Oracle 9.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_char)]  
  
 In questo esempio di query vengono restituiti i mapping predefiniti per il tipo di dati `NUMBER` di Oracle 9 quando viene specificato senza scala o precisione.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_number)]  
  
## <a name="see-also"></a>Vedere anche  
 [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Replica di database eterogenei](../non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Configurare un server di pubblicazione Oracle](../non-sql/configure-an-oracle-publisher.md)  
  
  
