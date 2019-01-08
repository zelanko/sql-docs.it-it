---
title: Specificare il formato dello snapshot (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e13b0635e750f8b6e59420fd25fe81af74eb7a0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811043"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>Specifica del formato dello snapshot (SQL Server Management Studio)
  Specificare il formato dello snapshot nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Per specificare il formato dello snapshot  
  
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare **Formato nativo di SQL Server: tutti i Sottoscrittori devono essere server che eseguono SQL Server** oppure **Carattere: obbligatorio se in un server di pubblicazione o in un Sottoscrittore non è in esecuzione SQL Server**.  
  
    > [!NOTE]  
    >  È consigliabile selezionare il formato nativo a meno che la pubblicazione non debba supportare sottoscrizioni a un database di [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o a un database non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà dello snapshot &#40;programmazione Transact-SQL della replica&#41;](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../initialize-a-subscription-with-a-snapshot.md)  
  
  
