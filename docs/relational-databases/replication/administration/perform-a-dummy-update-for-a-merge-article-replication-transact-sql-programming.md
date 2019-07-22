---
title: Eseguire un aggiornamento fittizio per un articolo di merge (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 38076ebad44e59d6004ac852486788a4b22c32f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939084"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>Esecuzione di un aggiornamento fittizio per un articolo di merge (programmazione Transact-SQL della replica)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replica di tipo merge utilizza i trigger come parte del processo di replica; in caso di aggiornamento di una tabella pubblicata, viene attivato un trigger di aggiornamento. In alcuni casi, i dati possono essere aggiornati senza l'attivazione del trigger, ad esempio durante le operazioni WRITETEXT e UPDATETEXT. In questi casi, è necessario aggiungere in modo esplicito un'istruzione UPDATE fittizia per replicare la modifica. È possibile aggiungere un'istruzione UPDATE fittizia utilizzando le stored procedure di replica.  
  
### <a name="to-add-a-dummy-update-statement"></a>Per aggiungere un'istruzione UPDATE fittizia  
  
1.  Eseguire l'operazione, ad esempio UPDATETEXT, su una riga in una tabella pubblicata di merge che richiede un aggiornamento fittizio.  
  
2.  Nel database del server di pubblicazione o del Sottoscrittore nel quale è stata apportata la modifica, eseguire [sp_mergedummyupdate &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md). Specificare la tabella nella quale è stata apportata la modifica per **@source_object** e l'identificatore univoco della riga modificata per **@rowguid** .  
  
3.  Sincronizzare la sottoscrizione per replicare la riga modificata.  
  
  
