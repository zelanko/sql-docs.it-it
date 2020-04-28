---
title: 'Esercitazione: SQL Server di file di dati nel servizio di archiviazione di Azure | Microsoft Docs'
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
ms.openlocfilehash: a15f6735ef0ef79b7eb953445c926f60f6bfb12e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176089"
---
# <a name="tutorial-sql-server-data-files-in-azure-storage-service"></a>Esercitazione: File di dati di SQL Server nel servizio Archiviazione di Azure
  Introduzione all'esercitazione relativa ai file di dati di SQL Server nel servizio di archiviazione di Azure. Questa esercitazione contiene informazioni utili sull'archiviazione dei file di dati di SQL Server direttamente nel servizio di archiviazione BLOB di Azure.  
  
 Il supporto per l'integrazione SQL Server per il servizio di archiviazione BLOB di Azure è un miglioramento SQL Server 2014. Per una panoramica delle funzionalità e dei vantaggi derivanti dall'uso di questa funzionalità, vedere [SQL Server di file di dati in Azure](databases/sql-server-data-files-in-microsoft-azure.md).  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 Questa esercitazione illustra come archiviare SQL Server file di dati nel servizio di archiviazione di Azure in più lezioni. Ogni lezione è incentrata su un'attività specifica. Per prima cosa, si apprenderà come creare un account di archiviazione e un contenitore in Azure. Si apprenderà quindi come creare una SQL Server credenziali per poter integrare SQL Server con archiviazione di Azure. Quindi, si creerà direttamente un database in archiviazione di Azure. Inoltre, verranno illustrati scenari di crittografia, di migrazione e di backup e ripristino.  
  
 L'esercitazione è suddivisa in nove lezioni:  
  
 **[Lezione 1: Creare account e contenitore di Archiviazione di Azure](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 In questa lezione viene creato un account di archiviazione di Azure e un contenitore.  
  
 **[Lezione 2. Creare un criterio per il contenitore e generare una firma di accesso condiviso &#40;chiave di&#41; SAS](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 In questa lezione vengono creati i criteri del contenitore BLOB e viene inoltre generata una firma di accesso condiviso.  
  
 **[Lezione 3: Creare le credenziali di SQL Server](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 In questa lezione verranno create le credenziali per archiviare le informazioni di sicurezza usate per accedere all'account di archiviazione di Azure.  
  
 **[Lezione 4: Creare un database in Archiviazione di Azure](../relational-databases/lesson-3-database-backup-to-url.md)**  
 In questa lezione viene creato un database in archiviazione di Azure usando l'opzione CREATE database FILENAME.  
  
 **[Lezione 5. &#40;facoltativo&#41; crittografare il database tramite Transparent Data Encryption](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 In questa lezione viene crittografato il database tramite Transparent Data Encryption (TDE) e un certificato del server.  
  
 **[Lezione 6: Eseguire la migrazione di un database da un computer di origine locale a un computer di destinazione in Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 In questa lezione viene eseguita la migrazione di un database da locale a una macchina virtuale in Azure tramite l'opzione CREATE DATABASE FOR Connetti.  
  
 **[Lezione 7: Spostare i file di dati in Archiviazione di Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 In questa lezione si spostano i file di dati in archiviazione di Azure usando l'istruzione ALTER DATABASE.  
  
 **[Lezione 8. Ripristinare un database in archiviazione di Azure](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 In questa lezione viene ripristinato un database in archiviazione di Azure utilizzando l'opzione RESTOre database MOVE.  
  
 **[Lezione 9. Ripristinare un database da archiviazione di Azure](lesson-8-restore-as-new-database-from-log-backup.md)**  
 In questa lezione viene ripristinato un database da archiviazione di Azure utilizzando l'opzione RESTOre database MOVE.  
  
## <a name="see-also"></a>Vedere anche  
 [File di dati di SQL Server in Azure](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
