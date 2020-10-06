---
description: gestione connessione SMO
title: Gestione connessione SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23a54cf3d07772276dbdf21dd7bf752a35121097
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91719442"
---
# <a name="smo-connection-manager"></a>gestione connessione SMO

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Una gestione connessione SMO consente a un pacchetto di connettersi a un server SMO (SQL Management Object). La gestione connessione SMO viene usata dalle attività di trasferimento incluse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. L'attività Trasferisci account di accesso, che trasferisce account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usa ad esempio una gestione connessione SMO.  
  
 Quando si aggiunge una gestione connessione SMO a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione SMO, imposta le proprietà di tale gestione connessione e quindi la aggiunge alla raccolta **Connessioni** del pacchetto. La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **SMOServer**.  
  
 Per configurare la gestione connessione SMO, procedere nel modo seguente:  
  
-   Specificare il nome del server in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Selezionare la modalità di autenticazione per la connessione al server.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configurazione della gestione connessione SMO  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione SMO]().  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="smo-connection-manager-editor"></a>Editor gestione connessione SMO
  L' **editor gestione connessione SMO** consente di configurare una connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che può essere utilizzata dalle varie attività di trasferimento di oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per ulteriori informazioni sulla gestione connessioni SMO, vedere [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome server**  
 Digitare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o selezionare il nome del server nell'elenco.  
  
 **Aggiorna**  
 Consente di aggiornare l'elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili che possono essere rilevate sulla rete.  
  
 **Usa autenticazione di Windows**  
 Consente di utilizzare l'autenticazione di Windows per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionata.  
  
 **Usa autenticazione di SQL Server**  
 Consente di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionata.  
  
 **Nome utente**  
 Se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere il nome utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Password**  
 Se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere la password.  
  
 **Test connessione**  
 Consente di testare la connessione configurata.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
