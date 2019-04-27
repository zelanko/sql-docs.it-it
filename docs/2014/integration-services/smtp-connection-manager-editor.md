---
title: Editor gestione connessione SMTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c4895a0fb7f3b64ff7db52aea9ab9319aeb8b9c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766494"
---
# <a name="smtp-connection-manager-editor"></a>Editor gestione connessione SMTP
  Usare la finestra di dialogo **Editor gestione connessioni SMTP** per specificare un server SMTP (Simple Mail Transfer Protocol).  
  
 Per ulteriori informazioni sulla gestione connessioni SMTP, vedere [SMTP Connection Manager](connection-manager/smtp-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **Name**  
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
>  Quando si usa Microsoft Exchange come server SMTP, potrebbe essere necessario impostare **usare l'autenticazione di Windows** a `True`. È possibile configurare i server Exchange in modo da impedire le connessioni SMTP non autenticate.  
  
 **Attiva SSL (Secure Sockets Layer)**  
 Selezionare questa opzione per crittografare le comunicazioni mediante SSL (Secure Sockets Layer) durante l'invio di messaggi di posta elettronica.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
