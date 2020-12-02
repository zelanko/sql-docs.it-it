---
title: Connetti ad Archiviazione di Microsoft Azure (Ripristino) | Microsoft Docs
description: In SQL Server la finestra di dialogo Account di archiviazione di Azure consente di specificare una connessione alle informazioni dell'account di archiviazione di Azure per ottenere l'archiviazione dei file in un account Azure.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 48bfc198e7e02a6382d149db144a0537d3e830a7
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130452"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Connetti ad Archiviazione di Microsoft Azure (Ripristino)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La finestra di dialogo consente di specificare la connessione alle informazioni sull'account di archiviazione di Azure per recuperare l'archivio di file nell'account di archiviazione di Azure. Dopo avere specificato le informazioni necessarie, fare clic su **Connetti** per stabilire la connessione all'archiviazione di Azure.  
  
## <a name="azure-storage-account"></a>Account di archiviazione di Azure  
 **Account di archiviazione**  
 Selezionare, digitare o incollare il nome dell'account di archiviazione di Azure da usare. Nella casella di riepilogo sono elencati gli account utilizzati in precedenza.  
  
 **Chiave dell'account**  
 Specificare la chiave di accesso dell'account di archiviazione di Azure.  
  
 Casella di controllo **Usa endpoint sicuri (HTTPS)**  
 Selezionare questa opzione per stabilire una connessione sicura all'archiviazione di Azure (scelta consigliata).  
  
 Casella di controllo **Salva chiave account**  
 Selezionare questa casella di controllo se si desidera memorizzare in SQL Server la chiave di accesso per l'account di archiviazione.  
  
### <a name="sql-credential"></a>Credenziali SQL  
 **Selezionare credenziali esistenti**  
 Selezionare le credenziali SQL esistenti corrispondenti alle informazioni sulla chiave account e sull'account di archiviazione.  
  
 **Crea nuove credenziali**  
 Selezionare questa opzione per creare nuove credenziali utilizzando le informazioni sulla chiave account e sull'account di archiviazione. Specificare il nome delle nuove credenziali nel campo **Nome credenziali** .  
  
  
