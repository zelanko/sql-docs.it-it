---
title: Creare un controllo del server e una specifica del controllo del database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6b4aa4358259492e1b49672b054eddb8713c7473
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211980"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>Creazione di un controllo del server e di una specifica del controllo del database
  In questo argomento viene illustrato come creare un controllo del server e la specifica di un controllo del database in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Il*controllo* di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comporta il rilevamento e la registrazione di eventi che si verificano nel sistema. L'oggetto *SQL Server Audit* raccoglie un'unica istanza di azioni a livello di server o di database e gruppi di azioni da monitorare. Il controllo si trova a livello dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile disporre di più controlli. Anche l'oggetto *Database-Level Audit Specification* fa parte di un controllo. È possibile creare una specifica del controllo del database per ogni database di SQL Server e per ogni controllo. Per altre informazioni, vedere [SQL Server Audit &#40;Motore di database&#41;](sql-server-audit-database-engine.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un controllo del server e una specifica del controllo del database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Le specifiche del controllo del database sono oggetti non a sicurezza diretta che risiedono in un database specifico. Quando una specifica del controllo del database viene creata, il relativo stato è disabilitato.  
  
 Durante la creazione o la modifica di una specifica di controllo in un database utente, non includere azioni di controllo su oggetti con ambito server, come le viste di sistema. Se si includono oggetti con ambito server, verrà creato il controllo, ma gli oggetti con ambito server non saranno inclusi e non verranno restituiti errori. Per eseguire il controllo degli oggetti con ambito server, utilizzare una specifica di controllo database nel database master.  
  
 Le specifiche di controllo del database risiedono nel database dove sono create, ad eccezione del database di sistema `tempdb`.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
  
-   Gli utenti che dispongono dell'autorizzazione ALTER ANY DATABASE AUDIT possono creare specifiche del controllo del database e associarle a qualsiasi controllo.  
  
-   Dopo essere stata creata, la specifica di controllo del database può essere visualizzata dalle entità che dispongono delle autorizzazioni CONTROL SERVER, ALTER ANY DATABASE AUDIT o dell'account sysadmin.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>Per creare un controllo del server  
  
1.  In Esplora oggetti espandere la cartella **Sicurezza** .  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **controlli** e scegliere **nuovo controllo.**... Per altre informazioni, vedere [creare un controllo del server e una specifica del controllo del server](create-a-server-audit-and-server-audit-specification.md).  
  
3.  Una volta selezionate le opzioni, fare clic su **OK**.  
  
#### <a name="to-create-a-database-level-audit-specification"></a>Per creare una specifica del controllo a livello di database  
  
1.  In Esplora oggetti espandere il database in cui si desidera creare una nuova specifica del controllo.  
  
2.  Espandere la cartella **Sicurezza** .  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Specifiche controllo database** e selezionare **Nuova specifica controllo data base...**.  
  
     Nella finestra di dialogo **Crea specifica controllo database** sono disponibili le opzioni indicate di seguito.  
  
     **Nome**  
     Nome della specifica del controllo del database. Tale nome viene generato automaticamente quando si crea una nuova specifica del controllo del server, ma è modificabile.  
  
     **Controllo**  
     Nome di un controllo del database esistente. Digitare il nome del controllo o selezionarlo nell'elenco.  
  
     **Tipo di azione di controllo**  
     Specifica i gruppi di azioni di controllo a livello di database e le azioni di controllo da acquisire. Per l'elenco di gruppi di azioni di controllo a livello di database e di azioni di controllo e una descrizione degli eventi contenuti, vedere [Azioni e gruppi di azioni di SQL Server Audit](sql-server-audit-action-groups-and-actions.md).  
  
     **Schema dell'oggetto**  
     Consente di visualizzare lo schema per il **nome oggetto**specificato.  
  
     **nome oggetto**  
     Nome dell'oggetto da controllare. Tale opzione è disponibile solo per le azioni di controllo e non si applica ai gruppi di controllo.  
  
     **Puntini di sospensione (...)**  
     Consente di visualizzare la finestra di dialogo **Seleziona oggetti** per eseguire la ricerca e la selezione di un oggetto disponibile, in base all'opzione **Tipo di azione di controllo**.  
  
     **Nome entità**  
     Account per filtrare il controllo per l'oggetto da controllare.  
  
     **Puntini di sospensione (...)**  
     Viene visualizzata la finestra di dialogo **Seleziona oggetti** per eseguire la ricerca e selezionare un oggetto disponibile, in base all'opzione **Nome oggetto**specificata.  
  
4.  Una volta selezionate le opzioni, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>Per creare un controllo del server  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>Per creare una specifica del controllo a livello di database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio seguente viene creata una specifica del controllo del database denominata `Audit_Pay_Tables` che controlla le istruzioni SELECT e INSERT per l'utente `dbo` per la tabella `HumanResources.EmployeePayHistory` in base al controllo del server definito in precedenza.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 Per altre informazioni, vedere [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql) e [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql).  
  
  
