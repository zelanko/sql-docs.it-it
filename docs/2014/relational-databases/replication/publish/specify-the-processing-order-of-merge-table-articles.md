---
title: Specificare l'ordine di elaborazione degli articoli di tabelle di Merge (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fbc61994e251063fe6d23450582d44c77616a662
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795573"
---
# <a name="specify-the-processing-order-of-merge-table-articles-replication-transact-sql-programming"></a>Impostazione dell'ordine di elaborazione degli articoli di tabelle di merge (programmazione Transact-SQL della replica)
  La replica di tipo merge consente di specificare l'ordine in cui gli articoli vengono elaborati dall'agente di merge durante il processo di sincronizzazione. È possibile assegnare a livello di programmazione un ordine a ogni articolo creato utilizzando le stored procedure di replica. Gli articoli vengono elaborati in ordine crescente in base al valore. Se due articoli hanno lo stesso valore, essi vengono elaborati simultaneamente. Per altre informazioni, vedere [Specificare l'ordine di elaborazione degli articoli di merge](../merge/specify-the-processing-order-of-merge-articles.md).  
  
### <a name="to-specify-the-processing-order-for-a-new-merge-article"></a>Per specificare l'ordine di elaborazione di un nuovo articolo di merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Specificare un valore integer che rappresenta l'ordine di elaborazione per l'articolo per **@processing_order**. Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
    > [!NOTE]  
    >  Quando si creano articoli ordinati, è necessario lasciare gap tra i valori relativi all'ordine degli articoli. In questo modo risulta più agevole impostare nuovi valori in futuro. Se ad esempio si dispone di tre articoli per cui è necessario specificare un ordine di elaborazione fisso, impostare il valore di **@processing_order** su 10, 20 e 30 anziché rispettivamente su 1, 2 e 3.  
  
### <a name="to-change-the-processing-order-of-a-merge-article"></a>Per modificare l'ordine di elaborazione di un articolo di merge  
  
1.  Per determinare l'ordine di elaborazione di un articolo, eseguire [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e prendere nota del valore di **processing_order** nel set di risultati.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore **processing_order** per **@property** e un valore integer che rappresenta l'ordine di elaborazione per **@value**.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare l'ordine di elaborazione degli articoli di merge](../merge/specify-the-processing-order-of-merge-articles.md)  
  
  
