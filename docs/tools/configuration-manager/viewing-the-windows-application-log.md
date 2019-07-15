---
title: Visualizzazione del registro applicazioni di Windows | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- application logs [SQL Server]
- Windows application logs [SQL Server]
- viewing Windows application logs
- errors [SQL Server], logs
- system logs [SQL Server]
- security logs [SQL Server]
- displaying Windows application logs
- logs [SQL Server], Windows application logs
ms.assetid: f9853b74-7db7-47cc-b957-e49ed5bc0a1a
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: b325e16b708dd85f80a52377467a35605466d587
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728152"
---
# <a name="viewing-the-windows-application-log"></a>Visualizzazione del registro applicazioni di Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per l'utilizzo del registro applicazioni di Microsoft Windows, durante ogni sessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono scritti nuovi eventi in tale registro. A differenza di quanto avviene per il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non viene creato un nuovo registro applicazioni a ogni avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È possibile visualizzare e gestire il registro applicazioni di Windows tramite il Visualizzatore eventi di Windows o il Visualizzatore log di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Il Visualizzatore eventi consente di visualizzare tre tipi di registro.  
  
|Tipo di registro di Windows|Descrizione|  
|----------------------|-----------------|  
|Registro di sistema|Registra gli eventi rilevati dai componenti del sistema operativo Windows. Ad esempio, un errore di un driver o di un altro componente di sistema da caricare all'avvio viene inserito nel registro di sistema.|  
|Registro di sicurezza|Registra gli eventi di sicurezza, ad esempio i tentativi di accesso non riusciti. In questo modo è possibile tenere traccia delle modifiche apportate al sistema di sicurezza e identificare eventuali punti deboli. Ad esempio, è possibile inserire nel registro di sicurezza i tentativi di accesso al sistema, in base alle impostazioni di controllo specificate in User Manager.<br /><br /> Soltanto i membri del ruolo predefinito del server **sysadmin** possono visualizzare il registro di sicurezza.|  
|Registro applicazioni|Registra gli eventi rilevati dalle applicazioni. Ad esempio, è possibile che un'applicazione del database inserisca un errore di file nel registro applicazioni.|  
  
 Per ulteriori informazioni sull'utilizzo del Visualizzatore eventi, sulla gestione del registro applicazioni e sul relativo contenuto, vedere la documentazione di Windows.  
  
 **Per visualizzare il registro delle applicazioni di Windows**  
  
 [Visualizzazione del log applicazioni di &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
  
