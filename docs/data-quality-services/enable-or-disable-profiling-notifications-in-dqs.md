---
description: Abilitare o disabilitare le notifiche di profiling in DQS
title: Abilitare o disabilitare le notifiche di profiling in DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- enable notifications
- notifications,enable
- notifications,disable
ms.assetid: e439bb29-60cc-4afd-a79a-f629b8d843c1
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4595f034ad1a3c26f3991af21207bb02e4321769
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431313"
---
# <a name="enable-or-disable-profiling-notifications-in-dqs"></a>Abilitare o disabilitare le notifiche di profiling in DQS

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  In questo argomento viene descritto come abilitare o disabilitare le notifiche di profiling in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Per impostazione predefinita, le notifiche di profiling in DQS sono abilitate. Le notifiche di profiling forniscono informazioni importanti sull'origine dati e sull'efficacia dell'attività corrente in esecuzione sui dati. Per altre informazioni, vedere [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per abilitare le notifiche, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="enable-or-disable-profiling-notifications"></a><a name="Enable"></a> Abilitare o disabilitare le notifiche di profiling  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Configurazione**.  
  
3.  Fare clic sulla scheda **Impostazioni generali** .  
  
4.  Deselezionare o selezionare la casella di controllo **Abilita notifiche** per disabilitare o abilitare le notifiche di profiling per le varie attività in DQS.  
  
5.  Fare clic su **Close**.  
  
  
