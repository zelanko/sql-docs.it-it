---
title: 'Lezione 1: Creare oggetti di archiviazione di Azure | Microsoft Docs'
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
ms.openlocfilehash: 53fcba3401a6798fb865613470ba78aa05e9b6dd
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176102"
---
# <a name="lesson-1-create-azure-storage-objects"></a>Lezione 1: Creare oggetti di Archiviazione di Azure
  Prima di creare i backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'archiviazione del cloud, è necessario creare prima un account di archiviazione e, successivamente, un contenitore BLOB. Nella lezione 1 vengono illustrati i passaggi per accedere al portale di gestione di Azure, creando un account di archiviazione e un contenitore BLOB.  
  
## <a name="create-a-storage-account"></a>Creare un account di archiviazione  
 Per creare un account di archiviazione dal portale di gestione di Azure, seguire questa procedura:  
  
1.  Accedere al portale di gestione di Azure usando l'account. Se non si dispone di un account Azure, [visitare la versione di valutazione gratuita di 3 mesi di Azure](https://go.microsoft.com/fwlink/?LinkId=271927).  
  
     ![Schermata di accesso di Azure](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "Schermata di accesso di Azure")  
  
2.  Per creare un account di archiviazione, seguire le istruzioni dettagliate riportate in [questo](https://go.microsoft.com/fwlink/?LinkId=271926)articolo.  
  
3.  Passare all'account di archiviazione creato nel passaggio precedente. Dal centro inferiore della pagina Web fare clic su **Gestisci chiavi**. Verranno visualizzate le informazioni sull'account. Copiare il nome dell'account di archiviazione e le chiavi di accesso. Queste informazioni sono necessarie per creare le credenziali archiviate di SQL. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] queste informazioni vengono utilizzate per accedere all'account di archiviazione e per creare i backup.  
  
     ![Screenshot delle chiavi dell'account di archiviazione di Azure](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "Screenshot delle chiavi dell'account di archiviazione di Azure")  
  
    > [!NOTE]  
    >  Inoltre, è possibile creare un account di archiviazione a livello di programmazione tramite le API REST. Per altre informazioni, vedere [creare un account di archiviazione](https://go.microsoft.com/fwlink/?LinkId=271928).  
  
### <a name="create-a-blob-container"></a>Creare un contenitore BLOB  
 Un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono essere inclusi in un contenitore. Un account può contenere un numero illimitato di contenitori, tuttavia ne deve contenere almeno uno. In un contenitore è possibile archiviare un numero illimitato di BLOB.  
  
 Per creare un contenitore, attenersi ai passaggi seguenti:  
  
1.  Selezionare l'account di archiviazione, fare clic sulla scheda **contenitori** , quindi su **Aggiungi contenitore** nella parte inferiore della schermata che consente di aprire una nuova finestra di dialogo.  
  
     ![Creazione di un contenitore nel portale di gestione](../../2014/tutorials/media/backuptocloud.gif "Creazione di un contenitore nel portale di gestione")  
  
2.  Immettere il nome associato al contenitore. Prendere nota del nome del contenitore specificato. Queste informazioni vengono utilizzate nell'URL (percorso del file di backup) nelle istruzioni T-SQL nelle lezioni 3 e 4.  
  
3.  Selezionare privato per **tipo di accesso**. È consigliabile creare contenitori privati per proteggere i file di backup.  
  
     ![Creazione di un nuovo contenitore BLOB](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "Creazione di un nuovo contenitore BLOB")  
  
    > [!NOTE]  
    >  L'autenticazione per l'account di archiviazione è obbligatorio per il backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anche se si sceglie di creare un contenitore pubblico.  
    >   
    >  Inoltre, è possibile creare un contenitore a livello di programmazione tramite le API REST. Per altre informazioni, vedere [create container](https://go.microsoft.com/fwlink/?LinkId=271946).  
  
### <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Creare una credenziale](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)SQL Server.  
  
  
