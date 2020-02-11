---
title: Modificare le connessioni che utilizzano i protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk o NWLink IPX SPX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: cdbcaa39e3d9630bd4ea50919f31cdbb15a36d14
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093896"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Modificare le connessioni che usano i protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk o NWLink IPX/SPX
  Sono stati rilevati protocolli di connettività client/server non supportati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Le applicazioni client che utilizzano i protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol (RPC), AppleTalk o NWLink IPX/SPX devono effettuare la connessione utilizzando un protocollo supportato.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 I protocolli di rete Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk e NWLink IPX/SPX non sono supportati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per i client che in precedenza utilizzavano questi protocolli è necessario selezionare un protocollo diverso.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le applicazioni client in modo che utilizzino un protocollo supportato per la connessione al server. Se è stato installato un alias che utilizza uno dei protocolli non supportati, tale alias deve essere modificato in modo da utilizzare uno dei protocolli supportati.  
  
 Se la stringa di connessione dell'applicazione USA o carica in modo specifico uno di questi protocolli, specificando NETWORK = DBMSRPCN per RPC, NETWORK = DBMSADSN per AppleTalk o NETWORK = DBMSVINN per la proprietà Banyan VINES oppure usando un prefisso esplicito, ad esempio "SPX:*Server\Istanza*" per SPX, "BV:*Server*" per Banyan VINES, "ADSP:*server*" per AppleTalk o "RPC:*Server*" per il multiprotocollo, è necessario modificare l'applicazione per usare uno dei protocolli supportati.  
  
 Per ulteriori informazioni, vedere "Scelta di un Protocollo di rete" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
