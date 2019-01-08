---
title: Configurare WMI per mostrare lo stato del server in Strumenti SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2982dc2825b621248da9f9c29e4aad8ddfc51bd5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764393"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>Configurazione di WMI per mostrare lo stato del server in Strumenti SQL Server
  In questo argomento viene descritto come configurare WMI per mostrare lo stato del server negli strumenti di SQL Server in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Durante la connessione ai server i componenti Server registrati e Esplora oggetti di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], nonché Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , utilizzano Strumentazione gestione Windows (WMI) per ottenere lo stato dei servizi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent (MSSQLSERVER). Per visualizzare lo stato del servizio, l'utente deve disporre dei diritti per accedere in remoto all'oggetto WMI. Per configurare questa autorizzazione, nel server deve essere installato WMI.  
  
##  <a name="SSMSProcedure"></a> Per configurare le autorizzazioni WMI  
  
1.  Scegliere **Esegui** dal menu **Start**nel server remoto.  
  
2.  Nel **aperto** nella casella `wmimgmt.msc`, quindi fare clic su **OK**.  
  
3.  Nel programma **Windows Management Infrastructure** fare clic con il pulsante destro del mouse su **Controllo WMI (Locale)** e scegliere **Proprietà**.  
  
4.  Nella scheda **Sicurezza** della finestra di dialogo **Proprietà - Controllo WMI (Locale)** espandere **Radice**e fare clic su **CIMV2**.  
  
5.  Fare clic sul pulsante **Sicurezza** per aprire la finestra di dialogo **Sicurezza per ROOT\CIMV2** .  
  
6.  Aggiungere un gruppo o un utente alla casella **Nomi utente o gruppo** e selezionarlo.  
  
7.  Nel **le autorizzazioni per * * *\<utente o gruppo >* , quindi selezionare il **Consenti** colonna, per i **Abilita remoto** autorizzazione, per gli utenti a cui si desiderano in modalità remota rilevare lo stato del servizio.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio, arresto o sospensione del servizio SQL Server Agent](agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
