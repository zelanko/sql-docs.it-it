---
title: Creazione di un utente di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.GENERAL.F1
- sql12.swb.user.securables.f1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 97fc758c754f5fc8803e988d55147670fc3ff45b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055439"
---
# <a name="create-a-database-user"></a>Creazione di un utente di database
  In questo argomento viene descritto come creare un utente di database con mapping a un account di accesso in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. L'utente del database è l'identità dell'account di accesso quando è connesso a un database. Può utilizzare lo stesso nome dell'account, ma non si tratta di una condizione obbligatoria. In questo argomento si presuppone che esista già un account di accesso in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per informazioni su come creare un account di accesso, vedere [creare un account di accesso](create-a-login.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Background](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un utente di database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="background"></a>Informazioni di background sul <a name="Restrictions"></a>  
 Un utente è un'entità di sicurezza a livello di database. Affinché gli account di accesso possano eseguire la connessione al database, è necessario eseguirne il mapping a un utente di database. È possibile eseguire il mapping di un account di accesso a database diversi come utenti diversi, ma come un singolo utente per ogni database. In un database parzialmente indipendente, può essere creato un utente che non dispone di un account di accesso. Per altre informazioni sugli utenti di database indipendenti, vedere [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql). Se è abilitato l'utente guest in un database, un account di accesso di cui non è stato eseguito il mapping a un utente del database può accedere al database come utente guest.  
  
> [!IMPORTANT]  
>  L'utente guest è in genere disabilitato. Non abilitarlo, a meno che non sia strettamente necessario.  
  
 È possibile concedere autorizzazioni agli utenti, in quanto entità di sicurezza. L'ambito di un utente è il database. Affinché un account di accesso possa eseguire la connessione a un database specifico nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario eseguirne il mapping a un utente del database. Le autorizzazioni all'interno del database vengono concesse e negate all'utente del database, non all'account di accesso.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione `ALTER ANY USER` per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
##### <a name="to-create-a-database-user"></a>Per creare un utente del database  
  
1.  In Esplora oggetti espandere la cartella **Database** .  
  
2.  Espandere il database in cui si desidera creare il nuovo utente del database.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Sicurezza**, scegliere **Nuovo** e quindi **Utente...**.  
  
4.  Nella finestra di dialogo **utente database-nuovo** , nella pagina **generale** , selezionare uno dei seguenti tipi di utente nell'elenco **tipo di utente** : **utente SQL con account di accesso**, **utente SQL senza account di accesso**, **utente mappato a un certificato**, **utente mappato a una chiave asimmetrica**o **utente di Windows**.  
  
5.  Immettere un nome per il nuovo utente nella casella **Nuovo utente** . Se è stato scelto **utente di Windows** dall' **elenco tipo di utente** , è anche possibile fare clic sui puntini di sospensione **(...)** per aprire la finestra di dialogo **Seleziona utente o gruppo** .  
  
6.  Nella casella **Nome account di accesso** immettere l'account di accesso per l'utente. In alternativa, fare clic sui puntini di sospensione **(...)** per aprire la finestra di dialogo **Seleziona account di accesso**. È disponibile**Nome account di accesso** se si seleziona **Utente SQL con account di accesso** o **Utente di Windows** dall'elenco **Tipo di utente** .  
  
7.  Nella casella **Schema predefinito** è specificato lo schema che diventerà proprietario degli oggetti creati da questo utente. In alternativa, fare clic sui puntini di sospensione **(...)** per aprire la finestra di dialogo **Seleziona schema**. È disponibile**Schema predefinito** se si seleziona **Utente SQL con account di accesso**, **Utente SQL senza account di accesso**o **Utente di Windows** nell'elenco **Tipo di utente** .  
  
8.  Nella casella **Nome certificato** , immettere il certificato da utilizzare per l'utente del database. In alternativa, fare clic sui puntini di sospensione **(...)** per aprire la finestra di dialogo **Seleziona certificato**. È disponibile**Nome certificato** se si seleziona **Utente con mapping eseguito a un certificato** dall'elenco **Tipo di utente** .  
  
9. Nella casella **Nome chiave asimmetrica**  , immettere la chiave da usare per l'utente del database. In alternativa, fare clic sui puntini di sospensione **(...)** per aprire la finestra di dialogo **Seleziona chiave asimmetrica**. È disponibile**Nome chiave asimmetrica** se si seleziona **Utente con mapping eseguito a una chiave asimmetrica** dall'elenco **Tipo di utente** .  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opzioni aggiuntive  
 La finestra di dialogo **Utente database - Nuovo** presenta diverse opzioni anche in altre quattro pagine: **Schemi di proprietà**, **Appartenenza**, **Entità a protezione diretta** e **Proprietà estese**.  
  
-   Nella pagina **Schemi di proprietà** sono elencati tutti i possibili schemi che possono essere di proprietà del nuovo utente del database. Per aggiungere schemi o rimuoverli da un utente del database, in **Schemi di proprietà di questo utente**selezionare o deselezionare le caselle di controllo accanto agli schemi.  
  
-   Nella pagina **Appartenenza** sono elencati tutti i possibili ruoli di appartenenza al database che possono essere di proprietà del nuovo utente del database. Per aggiungere ruoli o rimuoverli da un utente del database, in **Appartenenza a ruoli del database**selezionare o deselezionare le caselle di controllo accanto ai ruoli.  
  
-   Nella pagina **Entità a protezione diretta** sono elencate tutte le possibili entità a protezione diretta e le autorizzazioni su quelle entità a protezione diretta che possono essere concesse all'account di accesso.  
  
-   La pagina **Proprietà estese** consente di aggiungere proprietà personalizzate a utenti di database. In questa pagina sono disponibili le opzioni seguenti.  
  
     **Database**  
     Consente di visualizzare il nome del database selezionato. Questo campo è di sola lettura.  
  
     **Regole di confronto**  
     Consente di visualizzare le regole di confronto utilizzate per il database selezionato. Questo campo è di sola lettura.  
  
     **Proprietà**  
     Consente di visualizzare o specificare le proprietà estese relative all'oggetto. Ogni proprietà estesa è composta da una coppia nome/valore di metadati associati all'oggetto.  
  
     **Puntini di sospensione (...)**  
     Fare clic sui puntini di sospensione **(…)** dopo **Valore** per visualizzare la finestra di dialogo **Valore per Proprietà estesa**. Digitare o visualizzare il valore della proprietà estesa in questa finestra di dimensioni maggiori. Per ulteriori informazioni, vedere [Finestra di dialogo Valore per proprietà estesa](../../databases/value-for-extended-property-dialog-box.md).  
  
     **Elimina**  
     Consente di eliminare la proprietà estesa selezionata.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-create-a-database-user"></a>Per creare un utente del database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Entità &#40;motore di database&#41;](principals-database-engine.md)  
  
  
