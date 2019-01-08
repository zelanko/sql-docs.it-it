---
title: Proprietà Sottoscrittore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e35b5020eef6b7a884a0490d882c82e2775c8952
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805783"
---
# <a name="subscriber-properties"></a>Proprietà Sottoscrittore
  La finestra di dialogo **Proprietà Sottoscrittore** contiene informazioni relative ai Sottoscrittori che eseguono versioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="options"></a>Opzioni  
 **Connessione dell'agente al Sottoscrittore**  
 Contesto nel quale l'agente di distribuzione e l'agente di merge eseguono la connessione dal server di distribuzione al Sottoscrittore. Questa opzione riguarda solo le versioni precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Selezionare **Rappresenta l'account del processo dell'agente** per eseguire connessioni al Sottoscrittore utilizzando il contesto dell'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel server di distribuzione oppure specificare **Autenticazione di SQL Server**e quindi immettere un valore per **Nome account di accesso** e **Password**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di selezionare **Rappresenta l'account del processo dell'agente**.  
  
 Per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive le informazioni sulla connessione vengono specificate per ogni sottoscrizione nella Creazione guidata nuova sottoscrizione e possono essere modificate nella finestra di dialogo **Proprietà sottoscrizione** .  
  
 **Pianificazioni agenti predefinite**  
 Pianificazione predefinita utilizzata nella Creazione guidata nuova sottoscrizione per i Sottoscrittori che eseguono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Varie**  
 Include informazioni sul Sottoscrittore e sul tipo di Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)   
 [Riferimento alle proprietà &#40;replica&#41;](properties-reference-replication.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
