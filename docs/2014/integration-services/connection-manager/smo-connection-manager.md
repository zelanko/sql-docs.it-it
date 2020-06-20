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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c38b1037e3e6e2e36dbe288682867d6b9f030545
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920462"
---
# <a name="smo-connection-manager"></a>gestione connessione SMO
  Una gestione connessione SMO consente a un pacchetto di connettersi a un server SMO (SQL Management Object). La gestione connessione SMO viene usata dalle attività di trasferimento incluse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. L'attività Trasferisci account di accesso, che trasferisce account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usa ad esempio una gestione connessione SMO.  
  
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
  
  
