---
title: Gestione connessione WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d57a0783c8af0121169f09622b8e5bd8547d1ad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833087"
---
# <a name="wmi-connection-manager"></a>Gestione connessione WMI
  Una gestione connessione WMI consente a un pacchetto di utilizzare WMI (Windows Management Instrumentation, Strumentazione gestione Windows) per la gestione delle informazioni in un ambiente aziendale. La gestione connessione WMI viene usata dall'attività Servizio Web inclusa in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Quando si aggiunge una gestione connessione WMI a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione WMI, imposta le proprietà della gestione connessione e la aggiunge alla `Connections` raccolta del pacchetto. La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `WMI`.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Configurazione della gestione connessione WMI  
 Per configurare una gestione connessione WMI, procedere nel modo seguente:  
  
-   Specificare il nome di un server.  
  
-   Specificare uno spazio dei nomi sul server.  
  
-   Selezionare la modalità di autenticazione per la connessione al server.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione WMI](../wmi-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Attività servizio Web](../control-flow/web-service-task.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
