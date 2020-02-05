---
title: Posizionare dati e file di log in unità distinte | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54f469f8ab9f0daaf6f37c8f6bad1878bc716dbd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68086935"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>Posizionamento di dati e file di log in unità distinte
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare se i dati e i file di log si trovano in unità logiche distinte. Il posizionamento dei dati E dei file di log nello stesso dispositivo può provocare contesa nel dispositivo stesso, causando una riduzione delle prestazioni. Il posizionamento dei file in unità distinte fa sì che l'attività di I/O si verifichi contemporaneamente sia per i dati sia per i file di log.  
  
## <a name="recommendations"></a>Consigli  
 Quando si crea un nuovo database, specificare unità distinte per i dati e per i log. Per spostare i file una volta creato il database, è necessario che il database sia offline. Spostare i file usare uno dei metodi seguenti:  
  
> [!NOTE]  
>  Questi criteri non sono in grado di rilevare dispositivi fisici separati mediante punti di montaggio  
  
-   Ripristinare il database dal backup utilizzando l'istruzione RESTORE DATABASE con l'opzione WITH MOVE.  
  
-   Scollegare e quindi ricollegare il database specificando posizioni distinte per i dispositivi dei dati e dei log.  
  
-   Specificare una nuova posizione eseguendo l'istruzione ALTER DATABASE con l'opzione MODIFY FILE, riavviando quindi l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Spostare file del database](../../relational-databases/databases/move-database-files.md)  
  
 [Spostare database utente](../../relational-databases/databases/move-user-databases.md)  
  
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
