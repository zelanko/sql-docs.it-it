---
title: Creare uno schema di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3c3747149b23c6217f321eff9d19621189b89b66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011980"
---
# <a name="create-a-database-schema"></a>Creazione di uno schema di database
  In questo argomento si illustra come creare uno schema in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un schema mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Il nuovo schema è di proprietà di una delle seguenti entità a livello di database: utente di database, ruolo di database o ruolo applicazione. Gli oggetti creati all'interno di uno schema appartengono al proprietario dello schema e hanno un valore NULL per **principal_id** in **sys.objects**. La proprietà degli oggetti contenuti in uno schema può essere trasferita a qualsiasi entità a livello di database, ma il proprietario dello schema mantiene sempre l'autorizzazione CONTROL per gli oggetti all'interno dello schema.  
  
-   Quando si crea un oggetto di database, se si specifica un'entità di dominio valida (utente o gruppo) come proprietario dell'oggetto, l'entità di dominio sarà aggiunta al database come uno schema. Il proprietario del nuovo schema sarà l'entità di dominio.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
  
-   È richiesta l'autorizzazione CREATE SCHEMA per il database.  
  
-   Per specificare un altro utente come proprietario dello schema che viene creato, l'utente deve disporre dell'autorizzazione IMPERSONATE per quell'utente. Se si specifica un ruolo di database come proprietario, il chiamante deve disporre dell'appartenenza al ruolo oppure dell'autorizzazione ALTER per il ruolo.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>Per creare uno schema  
  
1.  In Esplora oggetti espandere la cartella **Database** .  
  
2.  Espandere il database in cui si desidera creare il nuovo schema di database.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Sicurezza** , scegliere **Nuovo**, quindi selezionare **Schema**.  
  
4.  Nella finestra di dialogo **Schema - Nuovo** della pagina **Generale** immettere un nome per il nuovo schema nella casella **Nome schema** .  
  
5.  Nella casella **Proprietario schema** immettere il nome di un utente o ruolo del database proprietario dello schema. In alternativa, fare clic su **Cerca** per aprire la finestra di dialogo **Cerca ruoli e utenti** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opzioni aggiuntive  
 La finestra di dialogo **Schema - Nuovo** offre anche opzioni in altre due pagine: **Autorizzazioni** e **Proprietà estese**.  
  
-   Nella pagina **Autorizzazioni** sono elencate tutte le possibili entità a protezione diretta e le autorizzazioni su quelle entità a protezione diretta che possono essere concesse all'account di accesso.  
  
-   La pagina **Proprietà estese** consente di aggiungere proprietà personalizzate a utenti di database.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-schema"></a>Per creare uno schema  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the schema Sprockets owned by Annik that contains table NineProngs.   
    -- The statement grants SELECT to Mandar and denies SELECT to Prasanna.  
  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE SCHEMA &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql).  
  
  
