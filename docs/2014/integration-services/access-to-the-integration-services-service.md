---
title: Servizio servizi di accesso per l'integrazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2ef77b0dac4db5b30eb12f3a857a3c25cb3caa57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62837439"
---
# <a name="access-to-the-integration-services-service"></a>Accesso al servizio Integration Services
  Tramite i livelli di protezione dei pacchetti è possibile limitare gli utenti a cui è consentito modificare ed eseguire un pacchetto. Per limitare gli utenti a cui è consentito visualizzare l'elenco di pacchetti attualmente in esecuzione in un server e arrestare i pacchetti attualmente in esecuzione in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]è necessaria una protezione aggiuntiva.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usa il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per visualizzare l'elenco dei pacchetti in esecuzione. I membri del gruppo Administrators di Windows possono visualizzare e arrestare tutti i pacchetti in esecuzione. Gli utenti che non appartengono a questo gruppo possono visualizzare e arrestare solo i pacchetti che hanno avviato personalmente.  
  
 È importante limitare l'accesso ai computer che eseguono un servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , soprattutto se si tratta di un servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che consente l'enumerazione di cartelle remote. Gli utenti autenticati possono richiedere l'enumerazione di pacchetti. Anche se il servizio non viene individuato, le cartelle vengono comunque enumerate dal servizio. Questi nomi di cartella potrebbero essere sfruttati da un utente malintenzionato. Se un amministratore ha configurato il servizio in modo da consentire l'enumerazione di cartelle in un computer remoto, agli utenti potrebbero essere visualizzati anche i nomi di cartella in genere non visibili.  
  
  
