---
title: Connessione ad archiviazione di Azure (ripristino) | Microsoft Docs
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
ms.openlocfilehash: 506f074a8693e54bdc51882ab08b19e9ea3e1994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876611"
---
# <a name="connect-to-windows-azure-storage-restore"></a>Connettersi al servizio di archiviazione Windows Azure (Ripristino)
  La finestra di dialogo consente di specificare la connessione alle informazioni sull'account del servizio di archiviazione Windows Azure per recuperare l'archiviazione di file nell'account di archiviazione di Windows Azure. Dopo avere specificato le informazioni necessarie, fare clic su **Connetti** per stabilire la connessione al servizio di archiviazione Microsoft Azure.  
  
## <a name="windows-azure-storage-account"></a>Account di archiviazione di Windows Azure  
 **Account di archiviazione**  
 Selezionare, digitare o incollare il nome dell'account di archiviazione di Windows Azure da utilizzare. Nella casella di riepilogo sono elencati gli account utilizzati in precedenza.  
  
 **Chiave dell'account**  
 Specificare la chiave di accesso dell'account di archiviazione di Windows Azure.  
  
 Casella di controllo**Usa endpoint sicuri (HTTPS)**  
 Selezionare questa opzione per stabilire una connessione sicura alla risorsa di archiviazione di Windows Azure (scelta consigliata).  
  
 Casella di controllo**Salva chiave account**  
 Selezionare questa casella di controllo se si desidera memorizzare in SQL Server la chiave di accesso per l'account di archiviazione.  
  
### <a name="sql-credential"></a>Credenziali SQL  
 **Selezionare credenziali esistenti**  
 Selezionare le credenziali SQL esistenti corrispondenti alle informazioni sulla chiave account e sull'account di archiviazione.  
  
 **Crea nuove credenziali**  
 Selezionare questa opzione per creare nuove credenziali utilizzando le informazioni sulla chiave account e sull'account di archiviazione. Specificare il nome delle nuove credenziali nel campo **Nome credenziali** .  
  
  
