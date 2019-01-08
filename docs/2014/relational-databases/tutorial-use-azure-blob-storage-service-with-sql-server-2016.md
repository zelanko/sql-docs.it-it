---
title: 'Esercitazione: File di dati di SQL Server nel servizio di archiviazione di Microsoft Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e3d33209cd6dfe261a5deced345adac70b46961f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810973"
---
# <a name="tutorial-sql-server-data-files-in-windows-azure-storage-service"></a>Esercitazione: File di dati di SQL Server nel Servizio di archiviazione di Microsoft Azure
  Introduzione all'esercitazione sui file di dati di SQL Server nel servizio di archiviazione Windows Azure In questa esercitazione sono incluse informazioni sull'archiviazione di file di dati di SQL Server direttamente nel servizio di archiviazione BLOB di Windows Azure.  
  
 Il supporto per l'integrazione di SQL Server per il servizio di archiviazione BLOB di Windows Azure è una funzionalità avanzata di SQL Server 2014. Per una panoramica delle funzionalità e vantaggi dell'uso di questa funzionalità, vedere [file di dati di SQL Server in Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md).  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 Nell'esercitazione viene illustrato come archiviare i file di dati di SQL Server nel servizio di archiviazione Windows Azure in più lezioni. Ogni lezione è incentrata su un'attività specifica. In primo luogo, verrà illustrato come creare un account di archiviazione e un contenitore in Windows Azure. Successivamente, verrà illustrato come creare le credenziali di SQL Server per poter integrare SQL Server con il Servizio di archiviazione Windows Azure. Infine, verrà creato un database direttamente nel Servizio di archiviazione Windows Azure. Inoltre, verranno illustrati scenari di crittografia, di migrazione e di backup e ripristino.  
  
 L'esercitazione è suddivisa in nove lezioni:  
  
 **[Lezione 1: Creare il contenitore e Account di archiviazione di Azure di Windows](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 In questa lezione vengono creati un contenitore e un account di archiviazione di Windows Azure.  
  
 **[Lezione 2. Creare un criterio sul contenitore e generare una firma di accesso condiviso &#40;firma di accesso condiviso&#41; chiave](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 In questa lezione vengono creati i criteri del contenitore BLOB e viene inoltre generata una firma di accesso condiviso.  
  
 **[Lezione 3: Creare una credenziale di SQL Server](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 In questa lezione verranno create le credenziali per archiviare le informazioni di sicurezza utilizzate per accedere all'account di archiviazione di Windows Azure.  
  
 **[Lezione 4: Creare un database in archiviazione di Microsoft Azure](../relational-databases/lesson-3-database-backup-to-url.md)**  
 In questa lezione viene creato un database nel Servizio di archiviazione Windows Azure utilizzando l'opzione FILENAME di CREATE DATABASE.  
  
 **[Lezione 5. &#40;Facoltativo&#41; crittografare il database tramite Transparent Data Encryption](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 In questa lezione viene crittografato il database tramite Transparent Data Encryption (TDE) e un certificato del server.  
  
 **[Lezione 6: Eseguire la migrazione di un database da un'origine del computer locale a una macchina di destinazione in Microsoft Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 In questa lezione viene eseguita la migrazione di un database da un'istanza locale a una macchina virtuale in Windows Azure utilizzando l'opzione FOR ATTACH di CREATE DATABASE.  
  
 **[Lezione 7: Spostare i file di dati in archiviazione di Microsoft Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 In questa lezione vengono spostati i file di dati nel Servizio di archiviazione Windows Azure utilizzando l'istruzione ALTER DATABASE.  
  
 **[Lezione 8. Ripristinare un database in archiviazione di Microsoft Azure](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 In questa lezione viene ripristinato un database nel Servizio di archiviazione Windows Azure utilizzando l'opzione MOVE di RESTORE DATABASE.  
  
 **[Lezione 9. Ripristinare un database da archiviazione di Microsoft Azure](lesson-8-restore-as-new-database-from-log-backup.md)**  
 In questa lezione viene ripristinato un database dal Servizio di archiviazione Windows Azure utilizzando l'opzione MOVE di RESTORE DATABASE.  
  
## <a name="see-also"></a>Vedere anche  
 [File di dati di SQL Server in Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
