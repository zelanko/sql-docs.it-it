---
title: Cerca server (Server di rete) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ffa52839c20a34574423e3b123da79f734fb69ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786690"
---
# <a name="browse-for-servers-network-servers"></a>Cerca server (Server di rete)
  Se si esegue la connessione a un componente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] senza conoscere il nome esatto dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], nella casella **Nome server** fare clic su **Cerca** per aprire la finestra di dialogo **Cerca server**.  
  
 Questa finestra di dialogo verrà popolata automaticamente dal servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser in esecuzione nei computer server. È possibile che il nome di un'istanza non compaia nell'elenco per diverse ragioni:  
  
-   Il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser potrebbe non essere in esecuzione nel computer sul quale è eseguito [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   La porta UDP 1434 potrebbe essere bloccata da un firewall.  
  
-   Il flag **HideInstance** potrebbe non essere impostato.  
  
 Per connettersi a un'istanza che non compare nell'elenco, digitare una stringa di connessione completa per l'istanza, compreso il numero della porta TCP/IP o il nome pipe delle named pipe.  
  
## <a name="options"></a>Opzioni  
 **Selezionare l'istanza di SQL Server in rete con cui stabilire la connessione**  
 Indicare il server a cui si desidera connettersi facendo clic sull'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] visualizzata nell'albero. È possibile visualizzare o nascondere parti della visualizzazione struttura ad albero, fare clic sui nodi contrassegnati con un **+** oppure **-** simbolo.  
  
  
