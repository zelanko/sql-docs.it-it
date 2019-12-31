---
title: 'Lezione 1: creare un account e un contenitore di archiviazione di Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbe773b8b8115cafc20bb60e962bfb42c9821636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253505"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>Lezione 1: creare un account e un contenitore di archiviazione di Azure
  Prima di poter iniziare a archiviare i file di dati SQL Server in archiviazione di Azure, è necessario creare prima un account di archiviazione di Azure e un contenitore BLOB e una firma di accesso condiviso. Nella lezione 1 vengono illustrati i passaggi per accedere al portale di gestione di Azure, creare un account di archiviazione, un contenitore BLOB e una firma di accesso condiviso.  
  
 Per impostazione predefinita, solo il proprietario dell'account di archiviazione può accedere a BLOB, tabelle e code all'interno dell'account. Per accedere alle risorse utilizzando questa nuova funzionalità di SQL Server senza condividere la chiave di accesso dell'account di archiviazione, è necessario eseguire le seguenti operazioni:  
  
-   Impostare le autorizzazioni del contenitore su privato.  
  
-   Creare una firma di accesso condivisa. Consente di delegare l'accesso limitato alla risorsa di un contenitore, un BLOB, una tabella o una coda specificando l'intervallo in cui le risorse sono disponibili e le relative autorizzazioni del client.  
  
-   Utilizzare i criteri di accesso archiviati per gestire le firme di accesso condivise di un contenitore o dei relativi BLOB. I criteri di accesso archiviati costituiscono una misura di controllo aggiuntiva sulle firme di accesso condivise e forniscono strumenti semplici per revocarli.  
  
 Per ulteriori informazioni, vedere [gestione dell'accesso alle risorse di archiviazione Azure](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx).  
  
## <a name="create-storage-account"></a>Crea account di archiviazione  
 Per creare un account di archiviazione nel portale di gestione di Azure, seguire questa procedura:  
  
1.  Accedere al portale di gestione di [Azure](https://manage.windowsazure.com) usando l'account. Se non si dispone di un account Azure, provare la [versione di valutazione gratuita di Azure](https://www.windowsazure.com/pricing/free-trial/).  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  Usare le istruzioni dettagliate per [creare un account di archiviazione](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). Si noti che quando si crea un account di archiviazione da usare per la funzionalità file di dati di SQL Server in Azure, è necessario deselezionare o disabilitare la replica geografica. Ciò si richiede perché l'ordine di scrittura non è garantito quando più BLOB partecipano alla replica a livello geografico. Se un account di archiviazione viene sottoposto alla replica a livello geografico ed è necessario il recupero, si verifica un errore.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>Creare un contenitore BLOB  
 In Azure un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono trovarsi in un contenitore. Un account di archiviazione può contenere un numero illimitato di contenitori, tuttavia ne deve contenere almeno uno. In un contenitore può essere archiviato un numero illimitato di BLOB. Per informazioni aggiornate sui limiti delle dimensioni di archiviazione, vedere [come usare il servizio di archiviazione BLOB di Azure in .NET](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/).  
  
 Per creare un contenitore in Azure, seguire questa procedura:  
  
1.  Accedere al [portale di gestione di Azure](https://manage.windowsazure.com).  
  
2.  Selezionare l'account di archiviazione, fare clic sulla scheda **contenitori** , quindi fare clic su **Aggiungi contenitore** nella parte inferiore della schermata, che consente di aprire una nuova finestra di dialogo.  
  
3.  Immettere un nome per il contenitore.  
  
4.  Selezionare **privato** per **tipo di accesso**. Quando si imposta l'accesso su privato, i dati del contenitore e del BLOB possono essere letti solo dal proprietario dell'account Azure.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  Per creare un contenitore a livello di programmazione è possibile utilizzare anche le API REST. Per altre informazioni, vedere [creare un contenitore](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) e informazioni di [riferimento sulle API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx).  
  
 **Lezione successiva:**  
  
 [Lezione 2. Creare un criterio per il contenitore e generare una firma di accesso condiviso &#40;chiave di&#41; SAS](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
