---
title: La promozione delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 893068965ab4566b6f6e4f78e39141de9be2b6ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63044307"
---
# <a name="transaction-promotion"></a>Promozione delle transazioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Transazione *promozione* descrive una transazione lightweight locale che può essere promossa automaticamente a una transazione completamente distribuibile in base alle esigenze. Quando una stored procedure gestita viene richiamata all'interno di una transazione del database sul server, il codice CLR (Common Language Runtime) viene eseguito nel contesto di una transazione locale.  Se all'interno di una transazione del database viene aperta una connessione a un server remoto, la connessione al server remoto viene inserita nella transazione distribuita e la transazione locale viene promossa automaticamente a una transazione distribuita. La promozione delle transazioni riduce pertanto l'overhead delle transazioni distribuite posticipando la creazione di una transazione distribuita finché non si rende necessaria. Tale promozione è automatica, se è stata abilitata mediante la **integra** (parola chiave) e non richiede un intervento da parte dello sviluppatore. Il Provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce il supporto per la promozione delle transazioni tramite le classi in .NET Framework **SqlClient** dello spazio dei nomi.  
  
## <a name="the-enlist-keyword"></a>Parola chiave Enlist  
 Il **ConnectionString** proprietà di un **SqlConnection** oggetto supporta la **integra** parola chiave, che indica se **SqlClient** individua i contesti transazionali e inserisce automaticamente la connessione in una transazione distribuita. Se questa parola chiave viene impostata su true (impostazione predefinita), la connessione viene inserita automaticamente nel contesto della transazione corrente del thread di apertura. Se invece la parola chiave viene impostata su false, la connessione SqlClient non interagisce con una transazione distribuita. Se **integra** non è specificato nella stringa di connessione, la connessione viene automaticamente inserita in una transazione distribuita se ne viene individuata una al momento dell'apertura della connessione.  
  
## <a name="distributed-transactions"></a>Transazioni distribuite  
 Le transazioni distribuite utilizzano in genere un numero elevato di risorse di sistema. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) gestisce tali transazioni e integra tutti gli strumenti di gestione delle risorse alle quali si accede dalle transazioni. Promozione delle transazioni, d'altra parte, è una forma speciale di un **System. Transactions** transazione che delega in modo efficiente il lavoro in una semplice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] delle transazioni. **System. Transactions**, **SqlClient**, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coordinano le operazioni relative alla gestione della transazione, promuovendola a una piena transazione distribuita in base alle esigenze.  
  
 Il vantaggio dell'uso di promozione delle transazioni è che quando viene aperta una connessione con un oggetto attivo **TransactionScope** transazione e non altre connessioni vengono aperte, del commit della transazione come transazione lightweight, anziché incorrere nell'overhead aggiuntivo di una piena transazione distribuita. Per altre informazioni sulle **TransactionScope**, vedere [usando System. Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione con CLR e transazioni](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
