---
title: Visualizzare il log applicazioni di Windows (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 72b47b9dada82f66ec0cb97b1f9a4dec8aebdbdf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748213"
---
# <a name="view-the-windows-application-log-windows"></a>Visualizzazione del log applicazioni di Windows
  Quando si configura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utilizzo del registro applicazioni di Windows, ogni sessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] scrive nuovi eventi in tale registro. A differenza di quanto avviene per il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non viene creato un nuovo registro applicazioni a ogni avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="to-view-the-windows-application-log"></a>Per visualizzare il registro delle applicazioni di Windows  
  
1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi**, **Strumenti di amministrazione**e quindi **Visualizzatore eventi**.  
  
2.  Nel Visualizzatore eventi fare clic su **Applicazione**.  
  
3.  Gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono contrassegnati dalla voce **MSSQLSERVER** (le istanze denominate sono contrassegnate dalla voce **MSSQL$***<nome_istanza>*) nella colonna **Origine**. Gli eventi di SQL Server Agent sono contrassegnati dalla voce SQLSERVERAGENT (per le istanze denominate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sono contrassegnati dalla voce **SQLAgent$**\<*instance_name*>). Gli eventi del servizio Microsoft Search sono contrassegnati dalla voce **Microsoft Search**.  
  
4.  Per visualizzare il registro di un altro computer, fare clic con il pulsante destro del mouse su **Visualizzatore eventi**, scegliere **Connetti a un altro computer** , quindi immettere le informazioni necessarie nella finestra di dialogo **Selezione computer**.  
  
5.  Facoltativamente, per visualizzare solo gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , scegliere **Filtro** dal menu **Visualizza**e quindi selezionare **MSSQLSERVER** nell'elenco **Origine evento**. Per visualizzare solo gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent selezionare invece **SQLSERVERAGENT** nell'elenco **Origine evento** .  
  
6.  Per visualizzare ulteriori informazioni su un evento, fare doppio clic sull'evento stesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzazione del log degli errori di SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
  
