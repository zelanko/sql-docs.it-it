---
title: Opzione di configurazione del server Timeout PH | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 25a89c00466cf4a702202f6a6fb4959f1d845c41
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639419"
---
# <a name="ph-timeout-server-configuration-option"></a>Opzione di configurazione del server PH timeout
  L'opzione PH timeout consente di specificare l'intervallo di tempo, in secondi, atteso dal gestore di protocollo full-text prima del timeout di una connessione a un database. Il valore predefinito è 60 secondi. Aumentare il valore di ph timeout quando i tentativi di connessione sono in timeout a causa di temporanei problemi di rete.  
  
 Il gestore di protocollo full-text è ospitato dall'host del daemon di filtri ed è utilizzato per recuperare da SQL Server i dati di cui eseguire l'indicizzazione full-text. Per altre informazioni sui componenti della ricerca full-text, vedere [Ricerca full-text](../../relational-databases/search/full-text-search.md).  
  
 Quando si tenta di recuperare una riga di dati, se il gestore del protocollo non può connettersi a SQL Server entro il periodo di tempo specificato, esso genera un errore di timeout per la riga. Il gatherer full-text ripeterà il tentativo sulla riga in un momento successivo. Per altre informazioni sul gatherer full-text, vedere [Popolamento degli indici full-text](../../relational-databases/indexes/indexes.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
