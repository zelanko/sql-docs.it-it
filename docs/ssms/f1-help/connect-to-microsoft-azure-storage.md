---
title: Connettersi al servizio di archiviazione Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f4b05cc0ebd3c3d230b5f42bb46b74885e8e1e6
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155675"
---
# <a name="connect-to-microsoft-azure-storage"></a>Connetti ad Archiviazione di Microsoft Azure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Usare la finestra di dialogo **Azure Storage Connection** (Connessione ad Archiviazione di Azure) per specificare un account di archiviazione e convalidare la connessione ad Azure.  
  
## <a name="options"></a>Opzioni  
Specificare le informazioni seguenti sull'account di Azure e fare clic su **Avanti** per continuare.  
  
1.  **Account di archiviazione** - specificare il nome dell'account di archiviazione.

   >[!NOTE]
   > È possibile connettersi solo agli [account di archiviazione di uso generico](https://docs.microsoft.com/azure/storage/storage-introduction#azure-storage-services). La connessione ad altri tipi di account di archiviazione può causare un errore simile al seguente:
   >
   >  Il valore per una delle intestazioni HTTP non è nel formato corretto. (Microsoft.SqlServer.StorageClient).
   >
   >  Errore del server remoto: (400) Richiesta errata. (Sistema)

2.  **Chiave account** - specificare la chiave account per l'account di archiviazione specificato.  
  
3.  **Usa endpoint sicuri (HTTPS)** - questa opzione usa la comunicazione crittografata e l'identificazione sicura di un server Web di rete.  
  
4.  **Salva chiave account** - questa opzione salva la password in un file crittografato.  
  
