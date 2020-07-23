---
title: Attività Notifica operatori | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0c23d46735f469680aa60d5667725b06c8e03536
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915250"
---
# <a name="notify-operator-task"></a>Notifica operatori - attività

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Notifica operatori consente di inviare messaggi di notifica agli operatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Un operatore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è l'alias di una persona o di un gruppo che può ricevere notifiche elettroniche. Per altre informazioni sugli operatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Operatori](../../ssms/agent/operators.md).  
  
 Grazie all'attività Notifica operatori, con un pacchetto possono essere inviate notifiche a uno o più operatori tramite posta elettronica, cercapersone o **Net Send**. Ogni operatore può ricevere notifiche tramite metodi diversi. È ad esempio possibile usare la posta elettronica e il cercapersone per inviare notifiche a OperatorA e usare il cercapersone e **Net Send**per inviare notifiche a OperatorB. Gli operatori che ricevono notifiche dall'attività devono essere membri della raccolta **OperatorNotify** per l'attività Notifica operatori.  
  
 L'attività Notifica operatori è l'unica attività di manutenzione del database che non incapsula istruzioni Transact-SQL o comandi DBCC.  
  
## <a name="configuration-of-the-notify-operator-task"></a>Configurazione dell'attività Notifica operatori  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Notifica operatori &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
