---
title: Modificare il tempo di recupero di riferimento di un database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9563f7ad61b33b4248ce22c58974d4967db6d55e
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584222"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>Modificare il tempo di recupero di riferimento di un database (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come impostare la modifica del tempo di recupero di riferimento di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per impostazione predefinita, il tempo di recupero di riferimento è 60 secondi e il database usa *checkpoint indiretti*. Il tempo di recupero di riferimento stabilisce un limite superiore per il tempo di recupero per questo database.  
  
> [!NOTE]  
>  Il limite superiore specificato per un determinato database dall'impostazione del tempo di recupero di riferimento può essere superato se una transazione con esecuzione prolungata provoca tempi eccessivi di UNDO.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
-   **Per modificare il tempo di recupero di riferimento tramite:**  [SQL Server Management Studio](#SSMSProcedure) o [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni 
  
> [!CAUTION]  
>  Un carico di lavoro transazionale online su un database configurato per i checkpoint indiretti potrebbe subire un calo delle prestazioni. I checkpoint indiretti assicurano che il numero di pagine dirty è inferiore a una determinata soglia, in modo che il recupero del database viene completato entro il tempo di recupero di riferimento. A differenza dei checkpoint indiretti, che usano il numero di pagine dirty, l'opzione di configurazione Intervallo di recupero usa il numero di transazioni per determinare il tempo di recupero. Quando i checkpoint indiretti sono abilitati per un database che riceve un numero elevato di operazioni DML, il writer in background può iniziare a scaricare i buffer dirty su disco in modo intensivo per garantire che il tempo necessario per eseguire il recupero non superi il tempo di recupero di riferimento impostato per il database. Questo può causare in determinati sistemi ulteriore attività di I/O che può comportare un collo di bottiglia delle prestazioni se il sottosistema del disco opera al di sopra o in prossimità della soglia di I/O.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per modificare il tempo di recupero di riferimento**  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espanderla.  
  
2.  Espandere il contenitore **Database**, quindi fare clic con il pulsante destro del mouse sul database da modificare e scegliere il comando **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà database** fare clic sulla pagina **Opzioni** .  
  
4.  Nel campo **Tempo di recupero di riferimento (secondi)** del pannello **Recupero** specificare un numero di secondi come limite superiore del tempo di recupero per il database.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per modificare il tempo di recupero di riferimento**  
  
1.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui risiede il database.  
  
2.  Usare l'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md), come indicato di seguito:  
  
     TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     A partire da [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)], il valore predefinito è 1 minuto. Se maggiore di 0 (impostazione predefinita per le versioni meno recenti), specifica il limite superiore per il tempo di recupero per il database specificato in caso di arresto anomalo.  
  
     SECONDS  
     Indica che *target_recovery_time* viene espresso come numero di secondi.  
  
     MINUTES  
     Indica che *target_recovery_time* viene espresso come numero di minuti.  
  
     Nell'esempio seguente viene impostato il tempo di recupero di riferimento del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] su `60` .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Checkpoint di database &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
