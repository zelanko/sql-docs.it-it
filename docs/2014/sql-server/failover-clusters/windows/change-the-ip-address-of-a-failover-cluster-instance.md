---
title: Modificare l'indirizzo IP di un'istanza del cluster di failover | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a9a93c9c6efdd5a864b5ab3ce0beacb7cbf1632
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049623"
---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>Modifica dell'indirizzo IP di un'istanza del cluster di failover
  In questo argomento viene descritto come modificare la risorsa indirizzo IP nell'istanza del cluster di failover (FCI) di AlwaysOn tramite lo snap-in Gestione cluster di failover. Lo snap-in Gestione cluster di failover è l'applicazione di gestione cluster per il servizio Windows Server Failover Clustering (WSFC).  
  
-   **Prima di iniziare:**  [Sicurezza](#Security)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Prima di iniziare, esaminare le informazioni seguenti [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] argomento della documentazione Online: [Before Installing Failover Clustering](../install/before-installing-failover-clustering.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per eseguire la manutenzione o l'aggiornamento di un'istanza FCI, è necessario essere un amministratore locale che dispone dell'account per accedere come servizio su tutti i nodi dell'istanza FCI.  
  
##  <a name="WSFC"></a> Utilizzo dello snap-in Gestione cluster di failover  
 **Per modificare la risorsa indirizzo IP per un'istanza FCI**  
  
1.  Aprire lo snap-in Gestione cluster di failover.  
  
2.  Espandere il nodo **Servizi e applicazioni** nel riquadro sinistro e fare clic sull'istanza FCI.  
  
3.  Nel riquadro a destra, nella categoria **Nome server** , fare clic con il pulsante destro del mouse sul'istanza di SQL Server e scegliere **Proprietà** per aprire la finestra di dialogo **Proprietà** .  
  
4.  Nella scheda **Generale** , modificare la risorsa indirizzo IP.  
  
5.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
6.  Nel riquadro destro fare clic con il pulsante destro del mouse su SQL IP Address1(nome dell'istanza del cluster di failover) e scegliere **Offline**. Lo stato di SQL IP Address1(nome dell'istanza del cluster di failover), di SQL Network Name(nome dell'istanza del cluster di failover) e di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] passerà da Online a Sospensione offline e quindi a Offline.  
  
7.  Nel riquadro destro fare clic con il pulsante destro del mouse su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]e scegliere **Online**. Lo stato di SQL IP Address1(nome dell'istanza del cluster di failover), di SQL Network Name(nome dell'istanza del cluster di failover) e di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] passerà da Offline a Sospensione online e quindi a Online.  
  
8.  Chiudere lo snap-in Gestione cluster di failover.  
  
  
