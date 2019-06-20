---
title: Creare un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], creating
- database creation [SQL Server], SQL Server Management Studio
- creating databases
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d93e6cfa3ce6e958b31c1156cd4fc5fa046ad5ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872327"
---
# <a name="create-a-database"></a>Creare un database
  In questo argomento si illustra come creare un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   In un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è possibile specificare al massimo 32.767 database.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   L'istruzione CREATE DATABASE deve essere eseguita in modalità autocommit, la modalità predefinita per la gestione delle transazioni, e non è consentita in una transazione esplicita o implicita.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Il backup del database [master](master-database.md) dovrebbe essere eseguito ogni volta che si crea, modifica o si rimuove un database utente.  
  
-   Durante la creazione di un database, creare file di dati di dimensioni corrispondenti alla quantità massima di dati che si prevede di includere nel database.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione CREATE DATABASE per il database master oppure l'autorizzazione CREATE ANY DATABASE o ALTER ANY DATABASE.  
  
 Per mantenere il controllo sull'utilizzo del disco per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'autorizzazione per la creazione dei database è in genere limitata a pochi account di accesso.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-database"></a>Per creare un database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Fare clic con il pulsante destro del mouse su **Database**, quindi scegliere **Nuovo database**.  
  
3.  In **Nuovo database**immettere un nome per il database.  
  
4.  Per creare il database accettando tutti i valori predefiniti, scegliere **OK**. In caso contrario, continuare con i passaggi facoltativi seguenti.  
  
5.  Per modificare il nome del proprietario, fare clic su ( **...** ) per selezionare un nome diverso.  
  
    > [!NOTE]  
    >  L'opzione **Usa indicizzazione full-text** è sempre selezionata e visualizzata in grigio, in quanto, a partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], tutti i database utente sono abilitati per la funzionalità full-text.  
  
6.  Per modificare i valori predefiniti dei file di dati primario e di log delle transazioni, fare clic sulla cella appropriata nella griglia **File di database** , quindi immettere il nuovo valore. Per ulteriori informazioni, vedere [Aggiungere file di dati o file di log a un database](add-data-or-log-files-to-a-database.md).  
  
7.  Per modificare le regole di confronto del database, selezionare la pagina **Opzioni** , quindi selezionare le regole di confronto nell'elenco.  
  
8.  Per modificare il modello di recupero, selezionare la pagina **Opzioni** , quindi selezionare un modello di recupero nell'elenco.  
  
9. Per modificare le opzioni di database, selezionare la pagina **Opzioni** , quindi modificare le opzioni di database. Per una descrizione di ogni opzione, vedere [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
10. Per aggiungere un nuovo filegroup, fare clic sulla pagina **Filegroup** . Fare clic su **Aggiungi** , quindi immettere i valori per il filegroup.  
  
11. Per aggiungere al database una proprietà estesa, selezionare la pagina **Proprietà estese** .  
  
    1.  Nella colonna **Nome** immettere un nome per la proprietà estesa.  
  
    2.  Nella colonna **Valore** immettere il testo della proprietà estesa. Immettere, ad esempio, una o più istruzioni tramite cui viene descritto il database.  
  
12. Per creare il database, scegliere **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-database"></a>Per creare un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si crea il database `Sales`. Dal momento che la parola chiave PRIMARY non è specificata, il primo file, cioè`Sales`_`dat`, corrisponde al file primario. Poiché nel parametro SIZE non viene specificato il suffisso MB o KB per le dimensioni del file `Sales`\_`dat` , viene utilizzato MB e le dimensioni del file vengono allocate in megabyte. Il backup del database `Sales`\_`log` vengono allocate in megabyte perché nel parametro `MB` è stato specificato in modo esplicito il suffisso `SIZE` .  
  
```sql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 Per altri esempi, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Filegroup e file di database](database-files-and-filegroups.md)   
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Add Data or Log Files to a Database](add-data-or-log-files-to-a-database.md)  
  
  
