---
title: Proprietà di rete di Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b9bb77c5139b299a25fbd75bc30a58790ee0c30
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072358"
---
# <a name="network-properties"></a>Proprietà di rete
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà del server elencate nelle tabelle seguenti. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Si applica a:** Modalità server multidimensionale e tabulare  
  
## <a name="general"></a>Generale  
 **ListenOnlyOnLocalConnections**  
 Proprietà booleana che stabilisce se lo stato di attesa viene applicato solo alle connessioni locali, ad esempio localhost.  
  
## <a name="listener"></a>Listener  
 **IPV4Support**  
 Proprietà a valore integer a 32 bit con segno che definisce il supporto per il protocollo IPv4. Questa proprietà può assumere uno dei valori elencati nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*0*|IPv4 disabilitato; i client non possono connettersi.|  
|*1*|(Impostazione predefinita) IPv4 non richiesto; il server non si avvia se non può restare in attesa di IPv4.|  
|*2*|Il protocollo IPv4 è facoltativo; il server prova a rimanere in attesa di IPv4 ma si avvia anche se non vi riesce.|  
  
 **IPV6Support**  
 Proprietà a valore integer a 32 bit con segno che definisce il supporto per il protocollo IPv6. Questa proprietà può assumere uno dei valori elencati nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*0*|IPv6 disabilitato; i client non possono connettersi.|  
|*1*|(Impostazione predefinita) IPv6 non richiesto; il server non si avvia se non può restare in attesa di IPv6.|  
|*2*|Il protocollo IPv6 è facoltativo; il server prova a rimanere in attesa di IPv6 ma si avvia anche se non vi riesce.|  
  
 **MaxAllowedRequestSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RequestSizeThreshold**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerReceiveTimeout**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerSendTimeout**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="requests"></a>Richieste  
 **EnableBinaryXML**  
 Proprietà booleana che stabilisce se il server riconoscerà il formato xml binario per richieste.  
  
 **EnableCompression**  
 Proprietà booleana che stabilisce se la compressione è abilitata per le richieste.  
  
## <a name="responses"></a>Responses  
 **CompressionLevel**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **EnableBinaryXML**  
 Proprietà booleana che stabilisce se il server è abilitato per risposte xml binarie.  
  
 **EnableCompression**  
 Proprietà booleana che stabilisce se la compressione è abilitata per risposte a richieste client.  
  
## <a name="tcp"></a>TCP  
 **InitialConnectTimeout**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxCompletedReceiveCount**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingAcceptExCount**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingReceiveCount**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingSendCount**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingAcceptExCount**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingReceiveCount**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ScatterReceiveMultiplier**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\DisableNonblockingMode**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\EnableLingerOnClose**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\EnableNagleAlgorithm**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\LingerTimeout**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ReceiveBufferSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\SendBufferSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
