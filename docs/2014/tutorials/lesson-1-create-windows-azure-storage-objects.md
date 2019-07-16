---
title: 'Lezione 1: Creare gli oggetti di archiviazione di Azure di Windows | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 449f86b80b93055bb23fe4cd32ace10e15724dbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210980"
---
# <a name="lesson-1-create-windows-azure-storage-objects"></a>Lezione 1: Creare oggetti di Archiviazione di Microsoft Azure
  Prima di creare i backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'archiviazione del cloud, è necessario creare prima un account di archiviazione e, successivamente, un contenitore BLOB. Nella lezione 1 vengono illustrati i passaggi per l'accesso al portale di gestione di Windows Azure e per la creazione di un account di archiviazione e di un contenitore BLOB.  
  
## <a name="create-a-storage-account"></a>Creare un account di archiviazione  
 Per creare un account di archiviazione dal portale di gestione di Windows Azure, attenersi ai passaggi seguenti:  
  
1.  Accedere al portale di gestione di Windows Azure utilizzando l'account. Se non hai un account di Windows Azure, [visita versione di valutazione gratuita di Windows Azure 3 mesi](https://go.microsoft.com/fwlink/?LinkId=271927).  
  
     ![Schermata di accesso ad Azure di Windows](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "schermata di accesso ad Azure di Windows")  
  
2.  Utilizzare le istruzioni passo passo dettagliate [qui](https://go.microsoft.com/fwlink/?LinkId=271926), per creare un account di archiviazione.  
  
3.  Passare all'account di archiviazione creato nel passaggio precedente. Da basso al centro della pagina web, fare clic su **GESTISCI CHIAVI**. Verranno visualizzate le informazioni sull'account. Copiare il nome dell'account di archiviazione e le chiavi di accesso. Queste informazioni sono necessarie per creare le credenziali archiviate di SQL. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] queste informazioni vengono utilizzate per accedere all'account di archiviazione e per creare i backup.  
  
     ![Cattura di schermata della finestra di Windows Azure Storage Account Keys](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "cattura di schermata della finestra di Windows Azure Storage Account Keys")  
  
    > [!NOTE]  
    >  Inoltre, è possibile creare un account di archiviazione a livello di programmazione tramite le API REST. Per altre informazioni, vedere [crea Account di archiviazione](https://go.microsoft.com/fwlink/?LinkId=271928).  
  
### <a name="create-a-blob-container"></a>Creare un contenitore BLOB  
 Un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono essere inclusi in un contenitore. Un account può contenere un numero illimitato di contenitori, tuttavia ne deve contenere almeno uno. In un contenitore è possibile archiviare un numero illimitato di BLOB.  
  
 Per creare un contenitore, attenersi ai passaggi seguenti:  
  
1.  Selezionare l'account di archiviazione, fare clic il **contenitori** scheda e fare clic su **Aggiungi contenitore** nella parte inferiore della schermata verrà aperta una nuova finestra di dialogo.  
  
     ![Creazione di un contenitore nel portale di gestione](../../2014/tutorials/media/backuptocloud.gif "crea un contenitore nel portale di gestione")  
  
2.  Immettere il nome associato al contenitore. Prendere nota del nome del contenitore specificato. Queste informazioni vengono utilizzate nell'URL (percorso del file di backup) nelle istruzioni T-SQL nelle lezioni 3 e 4.  
  
3.  Selezionare privato per **tipo di accesso**. È consigliabile creare contenitori privati per proteggere i file di backup.  
  
     ![Creazione di un nuovo contenitore blob](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "creando un nuovo contenitore blob")  
  
    > [!NOTE]  
    >  L'autenticazione per l'account di archiviazione è obbligatorio per il backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anche se si sceglie di creare un contenitore pubblico.  
    >   
    >  Inoltre, è possibile creare un contenitore a livello di programmazione tramite le API REST. Per altre informazioni, vedere [Create Container](https://go.microsoft.com/fwlink/?LinkId=271946).  
  
### <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Creare una credenziale di SQL Server](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md).  
  
  
