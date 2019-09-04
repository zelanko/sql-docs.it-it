---
title: Connetti ad Archiviazione di Microsoft Azure (Ripristino) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 94860f25b8cb53ab3c273da2e020d0d6a506ad0b
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155623"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Connetti ad Archiviazione di Microsoft Azure (Ripristino)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo consente di specificare la connessione alle informazioni sull'account di archiviazione di Azure per recuperare l'archivio di file nell'account di archiviazione di Azure. Dopo avere specificato le informazioni necessarie, fare clic su **Connetti** per stabilire la connessione all'archiviazione di Azure.  
  
## <a name="azure-storage-account"></a>Account di archiviazione di Microsoft Azure  
 **Account di archiviazione**  
 Selezionare, digitare o incollare il nome dell'account di archiviazione di Azure da usare. Nella casella di riepilogo sono elencati gli account utilizzati in precedenza.  
  
 **Chiave dell'account**  
 Specificare la chiave di accesso dell'account di archiviazione di Azure.  
  
 Casella di controllo**Usa endpoint sicuri (HTTPS)**  
 Selezionare questa opzione per stabilire una connessione sicura all'archiviazione di Azure (scelta consigliata).  
  
 Casella di controllo**Salva chiave account**  
 Selezionare questa casella di controllo se si desidera memorizzare in SQL Server la chiave di accesso per l'account di archiviazione.  
  
### <a name="sql-credential"></a>Credenziali SQL  
 **Selezionare credenziali esistenti**  
 Selezionare le credenziali SQL esistenti corrispondenti alle informazioni sulla chiave account e sull'account di archiviazione.  
  
 **Crea nuove credenziali**  
 Selezionare questa opzione per creare nuove credenziali utilizzando le informazioni sulla chiave account e sull'account di archiviazione. Specificare il nome delle nuove credenziali nel campo **Nome credenziali** .  
  
  
