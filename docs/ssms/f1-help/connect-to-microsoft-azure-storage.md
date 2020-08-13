---
title: Connetti ad Archiviazione di Microsoft Azure
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/12/2017
ms.openlocfilehash: f88bafe27da30ceec6154bf64cd9ced0046f7e87
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2020
ms.locfileid: "87123082"
---
# <a name="connect-to-microsoft-azure-storage"></a>Connetti ad Archiviazione di Microsoft Azure

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Usare la finestra di dialogo **Azure Storage Connection** (Connessione ad Archiviazione di Azure) per specificare un account di archiviazione e convalidare la connessione ad Azure.  
  
## <a name="options"></a>Opzioni  
Specificare le informazioni seguenti sull'account di Azure e selezionare **Avanti** per continuare.  
  
1.  **Account di archiviazione** - specificare il nome dell'account di archiviazione.

   >[!NOTE]
   > È possibile connettersi solo agli [account di archiviazione di uso generico](https://docs.microsoft.com/azure/storage/common/storage-introduction#azure-storage-services). La connessione ad altri tipi di account di archiviazione può causare un errore simile al seguente:
   >
   >  Il valore per una delle intestazioni HTTP non è nel formato corretto. (Microsoft.SqlServer.StorageClient).
   >
   >  Il server remoto ha restituito un errore: richiesta non valida (400). (Sistema)

2.  **Chiave account** - specificare la chiave account per l'account di archiviazione specificato.  
  
3.  **Usa endpoint sicuri (HTTPS)** - questa opzione usa la comunicazione crittografata e l'identificazione sicura di un server Web di rete.  
  
4.  **Salva chiave account** - questa opzione salva la password in un file crittografato.  
  
