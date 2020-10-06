---
description: Gestione connessione SMTP
title: Gestione connessione SMTP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smtpconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0609ea0b10cd5f656c78cbda8c3f2b7ad5be382f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91719246"
---
# <a name="smtp-connection-manager"></a>Gestione connessione SMTP

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Una gestione connessione SMTP consente a un pacchetto di connettersi a un server SMTP (Simple Mail Transfer Protocol). La gestione connessione SMTP viene usata dall'attività Invia messaggi inclusa in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Quando si utilizza Microsoft Exchange come server SMTP, potrebbe essere necessario configurare la gestione connessione SMTP per utilizzare l'autenticazione di Windows. È possibile configurare i server Exchange in modo da non consentire connessioni SMTP non autenticate.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Configurazione della gestione connessione SMTP  
 Quando si aggiunge una gestione connessione SMTP a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione SMTP, imposta le proprietà della gestione connessione e quindi la aggiunge alla raccolta **Connessioni** del pacchetto. La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **SMTP**.  
  
 Per configurare la gestione connessione SMTP, procedere nel modo seguente:  
  
-   Specificare una stringa di connessione.  
  
-   Specificare il nome di un server SMTP.  
  
-   Specificare il metodo di autenticazione da utilizzare.  
  
    > [!IMPORTANT]  
    >  La gestione connessione SMTP supporta solo l'autenticazione anonima e l'autenticazione di Windows. Non supporta l'autenticazione di base.  
  
-   Specificare se crittografare la comunicazione mediante TLS (Transport Layer Security), protocollo precedentemente noto come SSL (Secure Sockets Layer), quando si inviano messaggi di posta elettronica.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione SMTP]().  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="smtp-connection-manager-editor"></a>Editor gestione connessione SMTP
  Usare la finestra di dialogo **Editor gestione connessioni SMTP** per specificare un server SMTP (Simple Mail Transfer Protocol).  
  
 Per ulteriori informazioni sulla gestione connessioni SMTP, vedere [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare un nome univoco per la gestione connessione.  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la gestione connessione. È consigliabile includere nella descrizione informazioni sugli scopi della gestione connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Server SMTP**  
 Consente di specificare il nome del server SMTP.  
  
 **Usa autenticazione di Windows**  
 Selezionare questa opzione per inviare la posta elettronica mediante un server SMTM che utilizza l'autenticazione di Windows per consentire l'accesso.  
  
> [!IMPORTANT]  
>  La gestione connessione SMTP supporta solo l'autenticazione anonima e l'autenticazione di Windows. Non supporta l'autenticazione di base.  
  
> [!NOTE]  
>  Se si utilizza Microsoft Exchange come server SMTP, potrebbe essere necessario impostare l'opzione **Usa autenticazione di Windows** su **True**. È possibile configurare i server Exchange in modo da impedire le connessioni SMTP non autenticate.  
  
 **Attiva SSL (Secure Sockets Layer)**  
 Selezionare questa opzione per crittografare le comunicazioni tramite TLS/SSL durante l'invio di messaggi di posta elettronica.  
