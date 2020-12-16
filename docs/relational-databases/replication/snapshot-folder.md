---
description: Cartella snapshot
title: Cartella snapshot | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: cdb92210920bdc6287c690bbdad72ff666da111e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463182"
---
# <a name="snapshot-folder"></a>Cartella snapshot
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

La pagina **Cartella snapshot** viene visualizzata nella Configurazione guidata distribuzione e nella Creazione guidata nuova pubblicazione. Il percorso specificato per la cartella snapshot verrà utilizzato come percorso predefinito per tutti i server di pubblicazione abilitati nella procedura guidata. La cartella snapshot predefinita non si applica ai server di pubblicazione abilitati successivamente tramite la finestra di dialogo **Proprietà server di distribuzione** . Questa impostazione predefinita può essere sostituita per qualsiasi server di pubblicazione nella pagina **Server di pubblicazione** della Configurazione guidata distribuzione o della finestra di dialogo **Proprietà server di distribuzione** .  
  
La cartella snapshot è semplicemente una directory designata come condivisione. Gli agenti che eseguono letture e scritture in questa cartella devono disporre di autorizzazioni sufficienti per accedervi. Per altre informazioni sulle impostazioni di sicurezza appropriate per la cartella, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md). Prima di implementare la replica è necessario verificare che gli agenti di replica possano connettersi alla cartella snapshot. Accedere con l'account che verrà utilizzato da ogni agente e quindi tentare di accedere alla cartella snapshot.  

Per Istanza gestita di SQL di Azure, la cartella snapshot deve essere una condivisione file di Azure. 
  
## <a name="options"></a>Opzioni  
 **Cartella snapshot**  
 Consente di immettere il percorso della cartella in cui archiviare i file di snapshot.  
  
> [!NOTE]  
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di usare una condivisione di rete come percorso della cartella snapshot. I percorsi locali, ovvero quelli che iniziano con una lettera di unità, ad esempio C:\\, non sono accessibili agli agenti in altri computer.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le opzioni snapshot](../../relational-databases/replication/snapshot-options.md)   
 [Configura distribuzione](../../relational-databases/replication/configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
