---
title: Replicare le modifiche dello schema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bec2f363cd8c4f7dea45935568a88722b19323fc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060421"
---
# <a name="replicate-schema-changes"></a>Replica delle modifiche dello schema
  In questo argomento si illustra come replicare le modifiche dello schema in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Se si apportano le seguenti modifiche dello schema a un articolo pubblicato, per impostazione predefinita le modifiche vengono propagate ai Sottoscrittori di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   MODIFICA TABELLA  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
-   **Per replicare le modifiche dello schema, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   L'istruzione ALTER TABLE ... DROP COLUMN viene sempre replicata in tutti i Sottoscrittori la cui sottoscrizione contiene le colonne in corso di eliminazione, anche in caso di disabilitazione della replica delle modifiche dello schema.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Se non si desidera replicare le modifiche dello schema per una pubblicazione, disabilitare la replica delle modifiche dello schema nella finestra di dialogo **Proprietà pubblicazione- \<Publication> ** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-disable-replication-of-schema-changes"></a>Per disabilitare la replica delle modifiche dello schema  
  
1.  Nella pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione \<Publication> -** impostare il valore della proprietà **replica modifiche dello schema** su **false**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Per propagare soltanto modifiche dello schema specifiche, impostare la proprietà su **Vero** prima di una modifica dello schema e quindi impostarla su **Falso** al termine della modifica. Al contrario, per propagare la maggior parte delle modifiche dello schema ma non una determinata modifica, impostare la proprietà su **Falso** prima della modifica dello schema e quindi impostarla su **Vero** al termine della modifica.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 È possibile utilizzare le stored procedure di replica per specificare se queste modifiche dello schema vengono replicate. La stored procedure utilizzata dipende del tipo di pubblicazione.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>Per creare una pubblicazione snapshot o transazionale che non replica le modifiche dello schema  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addpublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), specificando il valore **0** per ** \@ replicate_ddl**. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>Per creare una pubblicazione di tipo merge che non replica le modifiche dello schema  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), specificando il valore **0** per ** \@ replicate_ddl**. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>Per disabilitare temporaneamente la replica delle modifiche dello schema per una pubblicazione snapshot o transazionale  
  
1.  Per una pubblicazione con replica delle modifiche dello schema, eseguire [sp_changepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), specificando il valore **replicate_ddl** per la ** \@ Proprietà** e il valore **0** per ** \@ value**.  
  
2.  Eseguire il comando DDL sull'oggetto pubblicato.  
  
3.  Opzionale Abilitare di nuovo la replica delle modifiche dello schema eseguendo [sp_changepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), specificando il valore **replicate_ddl** per la ** \@ Proprietà** e il valore **1** per ** \@ value**.  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>Per disabilitare temporaneamente la replica delle modifiche dello schema per una pubblicazione di tipo merge  
  
1.  Per una pubblicazione con replica delle modifiche dello schema, eseguire [sp_changemergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), specificando il valore **replicate_ddl** per la ** \@ Proprietà** e il valore **0** per ** \@ value**.  
  
2.  Eseguire il comando DDL sull'oggetto pubblicato.  
  
3.  Opzionale Abilitare di nuovo la replica delle modifiche dello schema eseguendo [sp_changemergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), specificando il valore **replicate_ddl** per la ** \@ Proprietà** e il valore **1** per ** \@ value**.  
  
## <a name="see-also"></a>Vedere anche  
 [Apportare modifiche allo schema nei database di pubblicazione](make-schema-changes-on-publication-databases.md)   
 [Apportare modifiche allo schema nei database di pubblicazione](make-schema-changes-on-publication-databases.md)  
  
  
