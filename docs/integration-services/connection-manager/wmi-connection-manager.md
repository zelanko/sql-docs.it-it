---
title: Gestione connessione WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 659eb7ee0c6e75c4df778d04b50b30efc35c3f97
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270624"
---
# <a name="wmi-connection-manager"></a>Gestione connessione WMI
  Una gestione connessione WMI consente a un pacchetto di utilizzare WMI (Windows Management Instrumentation, Strumentazione gestione Windows) per la gestione delle informazioni in un ambiente aziendale. Questa gestione connessione WMI è usata dall'attività Servizio Web inclusa in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Quando si aggiunge una gestione connessione WMI a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione WMI, imposta le proprietà di tale gestione connessione e quindi la aggiunge alla raccolta **Connessioni** del pacchetto. La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **WMI**.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Configurazione della gestione connessione WMI  
 Per configurare una gestione connessione WMI, procedere nel modo seguente:  
  
-   Specificare il nome di un server.  
  
-   Specificare uno spazio dei nomi sul server.  
  
-   Selezionare la modalità di autenticazione per la connessione al server.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="wmi-connection-manager-editor"></a>Editor gestione connessione WMI
  Usare la finestra di dialogo **Editor gestione connessioni WMI** per specificare una connessione del servizio Strumentazione gestione Windows (WMI) a un server.  
  
 Per ulteriori informazioni sulla gestione connessioni WMI, vedere [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare un nome univoco per la gestione connessione.  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la gestione connessione. È consigliabile includere nella descrizione informazioni sugli scopi della gestione connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Nome server**  
 Consente di specificare il nome del server al quale si desidera connettersi tramite WMI.  
  
 **Namespace**  
 Consente di specificare lo spazio dei nomi WMI.  
  
 **Usa autenticazione di Windows**  
 Selezionare questa opzione per utilizzare l'autenticazione di Windows. Se si utilizza l'autenticazione di Windows non è necessario specificare un nome utente o una password per la connessione.  
  
 **User name**  
 Se non si utilizza l'autenticazione di Windows è necessario specificare un nome utente per la connessione.  
  
 **Password**  
 Se non si utilizza l'autenticazione di Windows è necessario specificare una password per la connessione.  
  
 **Test**  
 Consente di verificare le impostazioni della gestione connessioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Servizio Web](../../integration-services/control-flow/web-service-task.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
