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
ms.openlocfilehash: 0ba5e4e5dd6d9a6541a98e0cb30229d7335bac24
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936082"
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
 Indicare il server a cui si desidera connettersi facendo clic sull'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] visualizzata nell'albero. È possibile mostrare o nascondere parti della visualizzazione albero facendo clic sui nodi contrassegnati con un **+** **-** simbolo o.  
  
  
