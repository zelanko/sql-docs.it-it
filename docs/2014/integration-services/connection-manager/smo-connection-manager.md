---
title: Gestione connessione SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85b202ed9914ce151b26d00d59ad9a84e96ef830
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804951"
---
# <a name="smo-connection-manager"></a>gestione connessione SMO
  Una gestione connessione SMO consente a un pacchetto di connettersi a un server SMO (SQL Management Object). Le attività di trasferimento incluse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usano una gestione connessione SMO. L'attività Trasferisci account di accesso, che trasferisce account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usa ad esempio una gestione connessione SMO.  
  
 Quando si aggiunge una gestione connessione SMO a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione SMO, imposta le proprietà di tale gestione connessione e quindi la aggiunge alla raccolta `Connections` del pacchetto. La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `SMOServer`.  
  
 Per configurare la gestione connessione SMO, procedere nel modo seguente:  
  
-   Specificare il nome del server in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Selezionare la modalità di autenticazione per la connessione al server.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configurazione della gestione connessione SMO  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione SMO](../smo-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
