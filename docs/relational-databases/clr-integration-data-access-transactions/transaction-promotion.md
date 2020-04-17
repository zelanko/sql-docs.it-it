---
title: Promozione delle transazioni Documenti Microsoft
description: Nell'integrazione CLR di SQL ServerSQL Server, una transazione locale leggera può essere promossa a transazione completamente distribuibile tramite l'innalzamento di livello delle transazioni.
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
ms.openlocfilehash: e77409f6bf6c71363e030f29f86f41205dd4a0f0
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487482"
---
# <a name="transaction-promotion"></a>Promozione delle transazioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La *promozione delle transazioni* descrive una transazione locale leggera che può essere promossa automaticamente a transazione completamente distribuibile in base alle esigenze. Quando una stored procedure gestita viene richiamata all'interno di una transazione del database sul server, il codice CLR (Common Language Runtime) viene eseguito nel contesto di una transazione locale.  Se all'interno di una transazione del database viene aperta una connessione a un server remoto, la connessione al server remoto viene inserita nella transazione distribuita e la transazione locale viene promossa automaticamente a una transazione distribuita. La promozione delle transazioni riduce pertanto l'overhead delle transazioni distribuite posticipando la creazione di una transazione distribuita finché non si rende necessaria. La promozione delle transazioni è automatica, se è stata abilitata utilizzando la parola chiave **Enlist** e non richiede l'intervento dello sviluppatore. Il provider di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .NET Framework per fornisce il supporto per l'innalzamento di livello delle transazioni, gestito tramite le classi nello spazio dei nomi **System.Data.SqlClient** di .NET Framework.  
  
## <a name="the-enlist-keyword"></a>Parola chiave Enlist  
 La proprietà **ConnectionString** di un oggetto **SqlConnection** supporta la parola chiave **Enlist** , che indica se **System.Data.SqlClient** rileva i contesti transazionali e inserisce automaticamente la connessione in una transazione distribuita. Se questa parola chiave viene impostata su true (impostazione predefinita), la connessione viene inserita automaticamente nel contesto della transazione corrente del thread di apertura. Se invece la parola chiave viene impostata su false, la connessione SqlClient non interagisce con una transazione distribuita. Se **Enlist** non è specificato nella stringa di connessione, la connessione viene automaticamente inserita in una transazione distribuita se ne viene rilevata una al momento dell'apertura della connessione.  
  
## <a name="distributed-transactions"></a>Transazioni distribuite  
 Le transazioni distribuite utilizzano in genere un numero elevato di risorse di sistema. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) gestisce tali transazioni e integra tutti gli strumenti di gestione delle risorse alle quali si accede dalle transazioni. La promozione delle transazioni, d'altra parte, è una forma speciale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una **transazione System.Transactions** che delega in modo efficace il lavoro a una transazione semplice. **System.Transactions**, **System.Data.SqlClient**e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coordinare il lavoro necessario per la gestione della transazione, promuovendola a transazione distribuita completa in base alle esigenze.  
  
 Il vantaggio dell'utilizzo dell'innalzamento di livello delle transazioni è che quando una connessione viene aperta con una transazione **TransactionScope** attiva e non vengono aperte altre connessioni, la transazione esegue il commit come transazione leggera, anziché incorrere nell'overhead aggiuntivo di una transazione distribuita completa. Per ulteriori informazioni su **TransactionScope**, vedere [Utilizzo di System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione con CLR e transazioni](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
