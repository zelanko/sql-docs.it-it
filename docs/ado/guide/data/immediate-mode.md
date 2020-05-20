---
title: Modalità immediata | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: rothja
ms.author: jroth
ms.openlocfilehash: d036b2fa33c2f9fd5696eeb2984d07d4217eff6e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757907"
---
# <a name="immediate-mode"></a>Modalità immediata
La modalità immediata è attiva quando la proprietà **LockType** è impostata su **adLockOptimistic** o **adLockPessimistic**. In modalità immediata le modifiche apportate a un record vengono propagate nell'origine dati non appena si dichiara il lavoro su una riga completa chiamando il metodo **Update** .  
  
## <a name="calling-update"></a>Chiamata di Update  
 Se si passa dal record che si aggiunge o si modifica prima di chiamare il metodo **Update** , ADO chiamerà automaticamente **Update** per salvare le modifiche. È necessario chiamare il metodo **CancelUpdate** prima della navigazione se si desidera annullare le modifiche apportate al record corrente o eliminare un record appena aggiunto.  
  
 Il record corrente rimane aggiornato dopo la chiamata al metodo **Update** .  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Utilizzare il metodo **CancelUpdate** per annullare tutte le modifiche apportate alla riga corrente o per eliminare una nuova riga aggiunta. Non è possibile annullare le modifiche apportate alla riga corrente o a una nuova riga dopo aver chiamato il metodo **Update** , a meno che le modifiche non facciano parte di una transazione di cui è possibile eseguire il rollback con il metodo **RollbackTrans** o parte di un aggiornamento batch. Nel caso di un aggiornamento batch, è possibile annullare l' **aggiornamento** con il metodo **CancelUpdate** o **CancelBatch** .  
  
 Se si aggiunge una nuova riga quando si chiama il metodo **CancelUpdate** , la riga corrente diventa la riga corrente prima della chiamata a **AddNew** .  
  
 Se la riga corrente non è stata modificata o è stata aggiunta una nuova riga, la chiamata del metodo **CancelUpdate** genera un errore.
