---
title: Modificare il tempo di recupero di riferimento di un database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 72ac6ac92da531d0f653e0fc03d88d170b7706e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62743217"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>Modificare il tempo di recupero di riferimento di un database (SQL Server)
  In questo argomento viene illustrato come impostare la modifica del tempo di recupero di riferimento di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per impostazione predefinita, il tempo di recupero di riferimento è 0 e il database utilizza *checkpoint automatici* (controllati dall'opzione server **recovery interval** ). L'impostazione del tempo di recupero di riferimento su un valore maggiore di 0 fa sì che il database utilizzi i *checkpoint indiretti* e stabilisce un limite superiore per il tempo di recupero per il database.  
  
> [!NOTE]  
>  Il limite superiore specificato per un determinato database dall'impostazione del tempo di recupero di riferimento può essere superato se una transazione con esecuzione prolungata provoca tempi eccessivi di UNDO.  
  
-   **Prima di iniziare:**  [limitazioni e restrizioni](#Restrictions), [sicurezza](#Security)  
  
-   **Per modificare il tempo di recupero di riferimento usando:**  [SQL Server Management Studio](#SSMSProcedure) o [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a>  
  
> [!CAUTION]  
>  Un carico di lavoro transazionale online su un database configurato per i checkpoint indiretti potrebbe subire un calo delle prestazioni. I checkpoint indiretti assicurano che il numero di pagine dirty è inferiore a una determinata soglia, in modo che il recupero del database viene completato entro il tempo di recupero di riferimento. A differenza dei checkpoint indiretti che usano il numero di pagine dirty, l'opzione di configurazione recovery interval usa il numero di transazioni per determinare il tempo di recupero. Quando i checkpoint indiretti sono abilitati per un database che riceve un numero elevato di operazioni DML, il writer in background può iniziare a scaricare i buffer dirty su disco in modo intensivo per garantire che il tempo necessario per eseguire il recupero non superi il tempo di recupero di riferimento impostato per il database. Questo può causare in determinati sistemi ulteriore attività di I/O che può comportare un collo di bottiglia delle prestazioni se il sottosistema del disco opera al di sopra o in prossimità della soglia di I/O.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 **Per modificare il tempo di recupero di riferimento**  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espanderla.  
  
2.  Fare clic con il pulsante destro del mouse sul database che si desidera modificare e scegliere il comando **Proprietà** .  
  
3.  Nella finestra di dialogo **Proprietà database** fare clic sulla pagina **Opzioni** .  
  
4.  Nel campo **Tempo di recupero di riferimento (secondi)** del pannello **Recupero** specificare il numero di secondi desiderato come limite superiore nel tempo di recupero per il database.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 **Per modificare il tempo di recupero di riferimento**  
  
1.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui risiede il database.  
  
2.  Usare l'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options), come indicato di seguito:  
  
     TARGET_RECOVERY_TIME **=** _TARGET_RECOVERY_TIME_ {seconds | MINUTI  
  
     *target_recovery_time*  
     Quando è maggiore di 0 (valore predefinito), il valore specifica il limite superiore del tempo di recupero per il database specificato in caso di arresto anomalo del sistema.  
  
     SECONDS  
     Indica che *target_recovery_time* viene espresso come numero di secondi.  
  
     MINUTES  
     Indica che *target_recovery_time* viene espresso come numero di minuti.  
  
     Nell'esempio seguente viene impostato il tempo di recupero di riferimento del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] su `60` .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Checkpoint di database &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
