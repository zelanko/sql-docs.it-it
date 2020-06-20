---
title: Cartella snapshot | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 48b490c65662edf65018e98dd1bc3339f6aae6b6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055622"
---
# <a name="snapshot-folder"></a>Cartella snapshot
  La pagina **Cartella snapshot** viene visualizzata nella Configurazione guidata distribuzione e nella Creazione guidata nuova pubblicazione. Il percorso specificato per la cartella snapshot verrà utilizzato come percorso predefinito per tutti i server di pubblicazione abilitati nella procedura guidata. La cartella snapshot predefinita non si applica ai server di pubblicazione abilitati successivamente tramite la finestra di dialogo **Proprietà server di distribuzione** . Questa impostazione predefinita può essere sostituita per qualsiasi server di pubblicazione nella pagina **Server di pubblicazione** della Configurazione guidata distribuzione o della finestra di dialogo **Proprietà server di distribuzione** .  
  
 La cartella snapshot è semplicemente una directory designata come condivisione. Gli agenti che eseguono letture e scritture in questa cartella devono disporre di autorizzazioni sufficienti per accedervi. Per altre informazioni sulle impostazioni di sicurezza appropriate per la cartella, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md). Prima di implementare la replica è necessario verificare che gli agenti di replica possano connettersi alla cartella snapshot. Accedere con l'account che verrà utilizzato da ogni agente e quindi tentare di accedere alla cartella snapshot.  
  
## <a name="options"></a>Opzioni  
 **Cartella snapshot**  
 Consente di immettere il percorso della cartella in cui archiviare i file di snapshot.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di usare una condivisione di rete come percorso della cartella snapshot. I percorsi locali, ovvero quelli che iniziano con una lettera di unità, ad esempio C:\\, non sono accessibili agli agenti in altri computer.  
  
## <a name="see-also"></a>Vedere anche  
 [Percorsi alternativi cartella snapshot](alternate-snapshot-folder-locations.md)   
 [Configurare la distribuzione](configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md)   
 [Visualizzare e modificare le proprietà del server di distribuzione e dell'editore](view-and-modify-distributor-and-publisher-properties.md)   
 [Inizializzazione di una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)  
  
  
