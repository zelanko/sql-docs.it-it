---
title: Opzione di configurazione del server Timeout PH | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3d918c816bc4a4053435fcd5d71f94c09f9c4ace
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67997929"
---
# <a name="ph-timeout-server-configuration-option"></a>Opzione di configurazione del server PH timeout
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'opzione PH timeout consente di specificare l'intervallo di tempo, in secondi, atteso dal gestore di protocollo full-text prima del timeout di una connessione a un database. Il valore predefinito è 60 secondi. Aumentare il valore di ph timeout quando i tentativi di connessione sono in timeout a causa di temporanei problemi di rete.  
  
 Il gestore di protocollo full-text è ospitato dall'host del daemon di filtri ed è utilizzato per recuperare da SQL Server i dati di cui eseguire l'indicizzazione full-text. Per altre informazioni sui componenti della ricerca full-text, vedere [Ricerca full-text](../../relational-databases/search/full-text-search.md).  
  
 Quando si tenta di recuperare una riga di dati, se il gestore del protocollo non può connettersi a SQL Server entro il periodo di tempo specificato, esso genera un errore di timeout per la riga. Il gatherer full-text ripeterà il tentativo sulla riga in un momento successivo. Per altre informazioni sul gatherer full-text, vedere [Popolamento degli indici full-text](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
