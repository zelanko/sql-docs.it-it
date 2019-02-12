---
title: 'Lezione 1: Creare Account di archiviazione di Azure di Windows e contenitori | Microsoft Docs'
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
ms.openlocfilehash: 8a1f8cef9f29c856ab0bc02480221e583a0078f3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039932"
---
# <a name="lesson-1-create-windows-azure-storage-account-and-container"></a>Lezione 1: creare un account e un contenitore di Archiviazione di Microsoft Azure
  Prima di poter avviare l'archiviazione di file di dati di SQL Server nel servizio di archiviazione Windows Azure, è innanzitutto necessario creare un account del servizio di archiviazione Windows Azure con un contenitore BLOB e una firma di accesso condivisa. Nella lezione 1 vengono illustrati i passaggi per l'accesso al portale di gestione di Windows Azure e per la creazione di un account di archiviazione, di un contenitore BLOB e di una firma di accesso condivisa.  
  
 Per impostazione predefinita, solo il proprietario dell'account di archiviazione può accedere ai BLOB, alle tabelle e alle code dell'account in uso. Per accedere alle risorse utilizzando questa nuova funzionalità di SQL Server senza condividere la chiave di accesso dell'account di archiviazione, è necessario eseguire le seguenti operazioni:  
  
-   Impostare le autorizzazioni del contenitore su privato.  
  
-   Creare una firma di accesso condivisa. Consente di delegare l'accesso limitato alla risorsa di un contenitore, un BLOB, una tabella o una coda specificando l'intervallo in cui le risorse sono disponibili e le relative autorizzazioni del client.  
  
-   Utilizzare i criteri di accesso archiviati per gestire le firme di accesso condivise di un contenitore o dei relativi BLOB. I criteri di accesso archiviati costituiscono una misura di controllo aggiuntiva sulle firme di accesso condivise e forniscono strumenti semplici per revocarli.  
  
 Per altre informazioni, vedere [gestire l'accesso alle risorse di archiviazione Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx).  
  
## <a name="create-storage-account"></a>Creare un account di archiviazione  
 Per creare un account di archiviazione nel portale di gestione di Windows Azure, effettuare i passaggi riportati di seguito:  
  
1.  Accedi per il [portale di gestione di Microsoft Azure](https://manage.windowsazure.com) utilizzando il proprio account. Se non hai un account di Azure, visitare [versione di valutazione gratuita di Windows Azure](http://www.windowsazure.com/pricing/free-trial/).  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  Usare le istruzioni passo a passo per [creare un account di archiviazione](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/). Si noti che quando si crea un account di archiviazione da utilizzare con la funzionalità relativa ai file di dati di SQL Server in Windows Azure, è necessario deselezionare o disabilitare la replica a livello geografico. Ciò si richiede perché l'ordine di scrittura non è garantito quando più BLOB partecipano alla replica a livello geografico. Se un account di archiviazione viene sottoposto alla replica a livello geografico ed è necessario il recupero, si verifica un errore.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>Creare un contenitore BLOB  
 In Windows Azure, un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono essere inclusi in un contenitore. Un account di archiviazione può contenere un numero illimitato di contenitori, tuttavia ne deve contenere almeno uno. In un contenitore è possibile archiviare un numero illimitato di BLOB. Per informazioni più aggiornate sui limiti di dimensioni di archiviazione, vedere [come usare il servizio di Windows Azure Blob Storage in .NET](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/).  
  
 Per creare un contenitore in Windows Azure, effettuare i passaggi riportati di seguito:  
  
1.  Accedi per il [portale di gestione Azure](https://manage.windowsazure.com).  
  
2.  Selezionare l'account di archiviazione, fare clic il **contenitori** scheda e fare clic su **Aggiungi contenitore** nella parte inferiore dello schermo, che apre una nuova finestra di dialogo.  
  
3.  Immettere un nome per il contenitore.  
  
4.  Selezionare **privati** per **tipo di accesso**. Quando si imposta l'accesso su privato, i dati del contenitore e del BLOB possono essere letti solo dal proprietario dell'account di Windows Azure.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  Per creare un contenitore a livello di programmazione è possibile utilizzare anche le API REST. Per altre informazioni, vedere [Create Container](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) nonché [riferimento all'API di Windows Azure Storage Services REST](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx).  
  
 **Lezione successiva:**  
  
 [Lezione 2: Creare un criterio sul contenitore e generare una firma di accesso condiviso &#40;firma di accesso condiviso&#41; chiave](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
  
