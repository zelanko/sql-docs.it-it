---
title: 'Esercitazione: Backup e ripristino di SQL Server nel servizio Archiviazione BLOB di Azure| Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b166930b5d077e7294fcdbc13449d40cab309425
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176121"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Esercitazione: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Azure
  Introduzione all'Introduzione con SQL Server backup e ripristino con il servizio di archiviazione BLOB di Azure. Questa esercitazione contiene nozioni utili sulla scrittura di backup nel servizio di archiviazione Blob di Azure e sul ripristino dallo stesso.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione viene illustrato come creare un account di archiviazione di Windows, un contenitore BLOB, la creazione di credenziali per l'accesso all'account di archiviazione, la scrittura di un backup nel servizio BLOB e l'esecuzione di un ripristino semplice. Questa esercitazione è suddivisa in quattro lezioni:  
  
 [Lezione 1: Creare oggetti di archiviazione di Azure](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 In questa lezione verranno creati un account di archiviazione e un contenitore BLOB di Azure.  
  
 [Lezione 2: Creazione di una credenziale SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 In questa lezione verranno create le credenziali per archiviare le informazioni di sicurezza usate per accedere all'account di archiviazione di Azure.  
  
 [Lezione 3: Scrivere un backup completo del database nel servizio di archiviazione BLOB di Azure](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 In questa lezione verrà eseguita un'istruzione T-SQL per scrivere un backup del database AdventureWorks2012 nel servizio di archiviazione BLOB di Azure.  
  
 [Lezione 4: Eseguire un ripristino da un backup completo del database](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 In questa lezione verrà eseguita un'istruzione T-SQL per il ripristino dal backup del database creato nella lezione precedente.  
  
### <a name="requirements"></a>Requisiti  
 Per completare l'esercitazione è necessario conoscere i concetti di backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e la sintassi T-SQL. Per utilizzare l'esercitazione, il sistema deve soddisfare i requisiti seguenti.  
  
-   Un'istanza di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e il database AdventureWorks2012 installati.  
  
     L'istanza di SQL Server può essere in locale o in una macchina virtuale di Azure.  
  
     È possibile utilizzare un database utente al posto di AdventureWorks2012 e modificare la sintassi tsql di conseguenza.  
  
-   All'account utente usato per eseguire i comandi BACKUP o RESTORE deve essere associato il ruolo del database **db_backup operator** con autorizzazioni **Modifica qualsiasi credenziale** .  
  
### <a name="additional-reading"></a>Ulteriori informazioni  
 Di seguito sono indicati alcuni argomenti consigliati per comprendere i concetti e le procedure consigliate quando si utilizza il servizio di archiviazione BLOB di Azure per i backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
1.  [SQL Server backup e ripristino con il servizio di archiviazione BLOB di Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
