---
title: Gestione connessione SMTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 948a7411c39191635245fdf0f6777538b1ef57fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833089"
---
# <a name="smtp-connection-manager"></a>Gestione connessione SMTP
  Una gestione connessione SMTP consente a un pacchetto di connettersi a un server SMTP (Simple Mail Transfer Protocol). Questa gestione connessione è usata dall'attività Invia messaggi inclusa in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Quando si utilizza Microsoft Exchange come server SMTP, potrebbe essere necessario configurare la gestione connessione SMTP per utilizzare l'autenticazione di Windows. È possibile configurare i server Exchange in modo da non consentire connessioni SMTP non autenticate.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Configurazione della gestione connessione SMTP  
 Quando si aggiunge una gestione connessione SMTP a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione SMTP, imposta le proprietà della gestione connessione e quindi la aggiunge alla raccolta `Connections` del pacchetto. La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `SMTP`.  
  
 Per configurare la gestione connessione SMTP, procedere nel modo seguente:  
  
-   Specificare una stringa di connessione.  
  
-   Specificare il nome di un server SMTP.  
  
-   Specificare il metodo di autenticazione da utilizzare.  
  
    > [!IMPORTANT]  
    >  La gestione connessione SMTP supporta solo l'autenticazione anonima e l'autenticazione di Windows. Non supporta l'autenticazione di base.  
  
-   Specificare se crittografare la comunicazione mediante SSL (Secure Sockets Layer) quando si inviano messaggi di posta elettronica.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione SMTP](../smtp-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
