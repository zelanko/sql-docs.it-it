---
title: Amministrare una topologia peer-to-peer (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3a73af1c1f3a7196d87f77681ee9d62a3ef248a4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068777"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>Amministrazione di una topologia peer-to-peer (programmazione Transact-SQL della replica)
  L'amministrazione di una topologia peer-to-peer è simile all'amministrazione di una tipica topologia di replica transazionale, sebbene diverse aree richiedano speciali considerazioni. La differenza principale nell'amministrazione di una topologia peer-to-peer consiste nella necessità di mettere il sistema in *stato di inattività*in caso di determinate modifiche. Mettere in stato di inattività un sistema significa arrestare le attività sulle tabelle pubblicate in tutti i nodi e verificare che ogni nodo abbia ricevuto tutte le modifiche dagli altri nodi. Per altre informazioni, vedere [Come mettere una topologia di replica in stato di inattività &#40;programmazione Transact-SQL della replica&#41;](quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
> [!NOTE]  
>  In una topologia peer-to-peer il database di distribuzione non può utilizzare una versione precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] rispetto a un Sottoscrittore pull.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>Per aggiungere un articolo a una configurazione esistente  
  
1.  Mettere in stato di inattività il sistema.  
  
2.  Arrestare l'agente di distribuzione in ciascun nodo nella topologia. Per altre informazioni, vedere [Concetti di base relativi ai file eseguibili dell’agente di replica](../concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Eseguire l'istruzione CREATE TABLE per aggiungere la tabella nuova a ogni nodo nella topologia.  
  
4.  Effettuare manualmente la copia bulk dei dati per la nuova tabella in tutti i nodi utilizzando l' [utilità bcp](../../../tools/bcp-utility.md).  
  
5.  Eseguire [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) per creare il nuovo articolo in ogni nodo nella topologia. Per altre informazioni, vedere [definire un articolo](../publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Dopo l'esecuzione di [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) , la replica aggiunge automaticamente l'articolo alle sottoscrizioni nella topologia.  
  
6.  Riavviare gli agenti di distribuzione in ciascun nodo nella topologia.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>Per apportare le modifiche dello schema nel database di pubblicazione  
  
1.  Mettere in stato di inattività il sistema.  
  
2.  Eseguire le istruzioni DLL (Data Definition Language) per modificare lo schema delle tabelle pubblicate. Per altre informazioni sulle modifiche dello schema supportate, vedere [Modifiche allo schema nei database di pubblicazione](../publish/make-schema-changes-on-publication-databases.md).  
  
3.  Prima di riprendere l'attività nelle tabelle pubblicate, mettere di nuovo il sistema in stato di inattività. Ciò garantisce che le modifiche dello schema siano ricevute da tutti i nodi prima che venga eseguita la replica di nuove modifiche dei dati.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è illustrato come aggiungere un nuovo articolo di tabella a una topologia di replica peer-to-peer esistente con due nodi.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createtables)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_cmdline)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createarticle)]  
  
## <a name="see-also"></a>Vedere anche  
 [Domande frequenti sull'amministrazione della replica](frequently-asked-questions-for-replication-administrators.md)   
 [Backup e ripristino di database SQL Server](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Replica transazionale peer-to-peer](../transactional/peer-to-peer-transactional-replication.md)  
  
  
