---
title: Proprietà Shared Memory | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bea56ada3ef490225fd08892128abb482b9342a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999535"
---
# <a name="shared-memory-properties"></a>Proprietà Shared Memory
  Usare la pagina **Protocollo** nella finestra di dialogo **Proprietà Shared Memory** per abilitare o disabilitare il protocollo Shared Memory. Shared Memory è il protocollo più semplice da utilizzare e non richiede la configurazione di impostazioni. Poiché i client che usano questo protocollo possono connettersi solo a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguita nello stesso computer, Shared Memory non è adatto per la maggior parte delle attività del database. Utilizzare il protocollo Shared Memory per la risoluzione dei problemi quando si sospetta che gli altri protocolli siano configurati in modo non corretto.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere riavviato per abilitare o disabilitare il protocollo.  
  
## <a name="options"></a>Opzioni  
 **Abilitata**  
 I valori possibili sono **Sì** e **No**. Il protocollo Shared Memory è attivato per impostazione predefinita.  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
