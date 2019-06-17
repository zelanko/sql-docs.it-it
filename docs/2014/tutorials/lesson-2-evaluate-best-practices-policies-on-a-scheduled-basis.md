---
title: 'Lezione 2: Valutare i criteri per procedure consigliate migliori in base a una pianificazione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29513ec37a946b9ec613ccc483048396149dd15a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042656"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>Lezione 2: Valutazione di criteri per procedure consigliate in base a una pianificazione
  È possibile configurare valutazioni pianificate di criteri per procedure consigliate in una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per configurare i criteri per procedure consigliate da eseguire in base a una pianificazione prestabilita, è necessario importare i criteri nell'istanza di destinazione.  
  
 Per distribuire criteri pianificati in più server, è possibile importare i criteri in un'istanza, configurare le pianificazioni per tutti i criteri, esportare i criteri pianificati in una cartella, quindi distribuire i criteri pianificati nelle istanze di destinazione tramite Server registrati.  
  
> [!IMPORTANT]  
>  Le istanze di destinazione devono eseguire [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versione successiva. Ai fini dell'automazione è necessario che i criteri siano archiviati localmente nell'istanza, operazione non supportata dalle versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
 In questa lezione verranno effettuate le operazioni seguenti:  
  
-   Importazione di criteri per procedure consigliate in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Configurazione di criteri da eseguire in base a una pianificazione.  
  
-   Distribuzione di criteri per procedure consigliate pianificati in più istanze mediante Server registrati.  
  
 In questa lezione sono inclusi gli argomenti seguenti:  
  
-   [Importazione dei criteri in un'istanza singola](../../2014/tutorials/import-the-policies-to-a-single-instance.md)  
  
-   [Pianificazione criteri](../../2014/tutorials/schedule-the-policies.md)  
  
-   [Distribuzione di criteri pianificati in istanze multiple](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare più server tramite server di gestione centrale](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
