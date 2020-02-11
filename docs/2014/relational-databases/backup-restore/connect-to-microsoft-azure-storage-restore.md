---
title: Connettersi ad archiviazione di Azure (ripristino) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fbb57fe629797e34cc7c61f224d65d46d4e66cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154768"
---
# <a name="connect-to-azure-storage-restore"></a>Connettersi ad Archiviazione di Azure (ripristino)
  La finestra di dialogo consente di specificare la connessione alle informazioni sull'account di archiviazione di Azure per recuperare l'archivio di file nell'account di archiviazione di Azure. Dopo avere specificato le informazioni necessarie, fare clic su **Connetti** per stabilire la connessione all'archiviazione di Azure.  
  
## <a name="azure-storage-account"></a>Account di archiviazione di Azure  
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
  
  
