---
title: Modificare le connessioni che usano protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk o NWLink IPX SPX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0cb9d235a02414b589735e7118bfe22f408d1d54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199971"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Modificare le connessioni che usano i protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk o NWLink IPX/SPX
  Sono stati rilevati protocolli di connettività client/server non supportati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Le applicazioni client che utilizzano i protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol (RPC), AppleTalk o NWLink IPX/SPX devono effettuare la connessione utilizzando un protocollo supportato.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 I protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk e NWLink IPX/SPX non sono supportati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per i client che in precedenza utilizzavano questi protocolli è necessario selezionare un protocollo diverso.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le applicazioni client in modo che utilizzino un protocollo supportato per la connessione al server. Se è stato installato un alias che utilizza uno dei protocolli non supportati, tale alias deve essere modificato in modo da utilizzare uno dei protocolli supportati.  
  
 Se la connessione all'applicazione di stringa in particolare utilizza o Carica uno di questi protocolli, per entrambe le reti specifica = DBMSRPCN per RPC, NETWORK = DBMSADSN per Appletalk o NETWORK = DBMSVINN per Banyan VINES proprietà, o utilizzando un prefisso esplicito quale "spx: *server\istanza*"per SPX," bv:*server*"per Banyan VINES," adsp:*server*"per AppleTalk, o" rpc:*server*"per Multiprotocol, quindi è necessario modificare l'applicazione per usare uno dei protocolli supportati.  
  
 Per ulteriori informazioni, vedere "Scelta di un Protocollo di rete" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
