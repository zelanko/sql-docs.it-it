---
title: Editor gestione connessione SMTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ca3da66a23292212df7464c8d5966e5c3603e13e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962941"
---
# <a name="smtp-connection-manager-editor"></a>Editor gestione connessione SMTP
  Usare la finestra di dialogo **Editor gestione connessioni SMTP** per specificare un server SMTP (Simple Mail Transfer Protocol).  
  
 Per ulteriori informazioni sulla gestione connessioni SMTP, vedere [SMTP Connection Manager](connection-manager/smtp-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
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
>  Quando si utilizza Microsoft Exchange come server SMTP, potrebbe essere necessario impostare **utilizza autenticazione di Windows** su `True` . È possibile configurare i server Exchange in modo da impedire le connessioni SMTP non autenticate.  
  
 **Attiva SSL (Secure Sockets Layer)**  
 Selezionare questa opzione per crittografare le comunicazioni mediante SSL (Secure Sockets Layer) durante l'invio di messaggi di posta elettronica.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
