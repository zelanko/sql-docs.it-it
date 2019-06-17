---
title: Preparazione dei database di Access per la migrazione (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 9495ff7a58da124255cc6bf5674d92ebeef4c2b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299474"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparazione dei database di Access per la migrazione (AccessToSQL)
Prima di migrare i database di Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario determinare i database di cui eseguire la migrazione e assicurarsi che tali database siano pronti per la migrazione.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinazione della necessità di eseguire la migrazione a SQL Server  
Il motore di database Jet, che viene utilizzato come il motore di database per l'accesso, è una soluzione flessibile e facile da usare per la gestione dei dati. Tuttavia, come i database diventi più grandi e più mission-critical, molti utenti individuare che richiedono prestazioni superiori, sicurezza o la disponibilità. Per le applicazioni che richiedono una più solida piattaforma di dati, prendere in considerazione lo spostamento di database sottostanti per tali applicazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sui casi in cui eseguire la migrazione, vedere la [pagina di informazioni di migrazione](https://go.microsoft.com/fwlink/?LinkId=68571) nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sito Web.  
  
Dopo la migrazione dei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a usare l'accesso usando le tabelle collegate o è possibile eseguire manualmente la migrazione delle applicazioni per [!INCLUDE[msCoName](../../includes/msconame_md.md)] codice basato su .NET Framework che interagisce direttamente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="determining-which-databases-to-migrate"></a>Determinazione di database di cui eseguire la migrazione  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per l'accesso può individuare i database di Access per l'utente. È quindi possibile esportare i metadati relativi a questi database al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni su come esportare ed eseguire query sui metadati, vedere [esportazione di un inventario di Access](exporting-an-access-inventory-accesstosql.md).  

   > [!NOTE]
   > Non tutte le funzionalità di accesso e le impostazioni sono supportate da, o possono essere facilmente convertite, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Prima di iniziare la migrazione dei database, vedere [funzionalità di accesso non compatibili](incompatible-access-features-accesstosql.md).
  
## <a name="preparing-for-migration"></a>Preparazione alla migrazione  
Usare le linee guida seguenti per preparare i database di Access per la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="upgrading-older-access-databases"></a>L'aggiornamento dei database di Access meno recenti  
SSMA for Access supporta Access 97 e versioni successive. Se sono presenti database da versioni precedenti di Access, aprire e salvare i database di Access 97 o versione successiva.  
  
### <a name="removing-workgroup-protection"></a>Rimozione della protezione del gruppo di lavoro  
SSMA non è possibile eseguire la migrazione di database che usano la protezione del gruppo di lavoro. Per rimuovere la protezione del gruppo di lavoro da un database di Access, procedere come segue:  
  
1.  Copiare il file di database di Access in un'altra posizione.  
  
2.  Aprire il database copiato.  
  
3.  Nel **degli strumenti** dal menu **Security**e quindi selezionare **autorizzazioni utenti e gruppi**.  
  
4.  Selezionare il **gli utenti** opzione, selezionare il **Admin** utente, quindi verificare che il **Administer** l'autorizzazione è selezionata.  
  
5.  Selezionare il **gruppi** opzione, selezionare la **utenti** gruppo e quindi verificare che il **Administer** l'autorizzazione è selezionata.  
  
6.  Fare clic su **OK**e quindi scegliere il **File** dal menu fare clic su **uscita**.  
  
È ora possibile usare SSMA per la migrazione del database copiato. Dopo aver caricato lo schema nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile proteggere il database manualmente su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="backing-up-databases"></a>Backup dei database  
Prima di eseguire la migrazione dei database di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è consigliabile eseguire il backup sia i database di Access che eseguirà la migrazione, nonché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database in cui verrà eseguita la migrazione di accesso dati e oggetti.  
  
Per eseguire il backup di un database di Access nel **degli strumenti** dal menu **utilità Database**e quindi selezionare **backup Database**.  
  
Per informazioni su come eseguire il backup [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database, vedere "backup e ripristino di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
### <a name="documenting-databases"></a>Documentazione di database  
È possibile anche documentare le proprietà, ad esempio elenchi di oggetti di database, le dimensioni dei file e autorizzazioni, i database di Access. Per generare questa documentazione in Access e nel **degli strumenti** dal menu **Analizza**e quindi fare clic su **documentazione**.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Collegamento delle applicazioni di accesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
