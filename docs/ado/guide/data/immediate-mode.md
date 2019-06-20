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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37ad4cbc60ad4c08b65ff7f0db9b5c70245a96e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700586"
---
# <a name="immediate-mode"></a>Modalità immediata
Modalità immediata è attiva quando la **LockType** è impostata su **adLockOptimistic** oppure **adLockPessimistic**. In modalità immediata, propagazione delle modifiche a un record nell'origine dati, non appena si dichiara il lavoro in una riga completa chiamando il **Update** (metodo).  
  
## <a name="calling-update"></a>Chiamata al metodo Update  
 Se si sposta dal record si aggiunge o modifica prima di chiamare il **Update** metodo, verrà automaticamente chiamato **Update** per salvare le modifiche. È necessario chiamare il **CancelUpdate** metodo prima dello spostamento se si desidera annullare eventuali modifiche apportate al record corrente oppure eliminare il record appena aggiunto.  
  
 Il record corrente rimane invariato dopo aver chiamato il **Update** (metodo).  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Usare la **CancelUpdate** metodo per annullare le modifiche apportate alla riga corrente oppure per eliminare una riga appena aggiunta. Non è possibile annullare le modifiche apportate alla riga corrente o a una nuova riga dopo la chiamata il **Update** metodo, a meno che le modifiche siano parte di una transazione di cui è possibile eseguire il rollback con la **RollbackTrans** metodo o in parte un aggiornamento batch. Nel caso di un aggiornamento batch, è possibile annullare il **aggiornare** con il **CancelUpdate** oppure **CancelBatch** (metodo).  
  
 Se si aggiunge una nuova riga quando si chiama il **CancelUpdate** metodo, la riga corrente diventa la riga corrente prima di **AddNew** chiamare.  
  
 Se non si hanno modificato la riga corrente o aggiunta una nuova riga, la chiamata di **CancelUpdate** metodo genera un errore.
