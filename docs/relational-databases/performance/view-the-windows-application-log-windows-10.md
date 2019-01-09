---
title: Visualizzare il registro applicazioni di Windows (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
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
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 4697609b0f7c28c082b9b6187f002ecb9b6d9b16
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367973"
---
# <a name="view-the-windows-application-log-windows-10"></a>Visualizzare il registro applicazioni di Windows (Windows 10)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si configura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utilizzo del registro applicazioni di Windows, ogni sessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] scrive nuovi eventi in tale registro. A differenza di quanto avviene per il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non viene creato un nuovo registro applicazioni a ogni avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="view-the-windows-application-log"></a>Visualizzare il log applicazioni di Windows  
  
1. Nella **barra di ricerca** digitare **Visualizzatore eventi**, quindi selezionare l'app desktop **Visualizzatore eventi**.
  
2. In **Visualizzatore eventi** aprire **Registri applicazioni e servizi**.

3. Gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono contrassegnati dalla voce **MSSQLSERVER** (le istanze denominate sono contrassegnate dalla voce **MSSQL$***<nome_istanza>*) nella colonna **Origine**. Gli eventi di SQL Server Agent sono contrassegnati dalla voce SQLSERVERAGENT (per le istanze denominate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sono contrassegnati dalla voce **SQLAgent$**\<*instance_name*>). Gli eventi del servizio Microsoft Search sono contrassegnati dalla voce **Microsoft Search**.  
  
4. Per visualizzare il registro di un altro computer, fare clic con il pulsante destro del mouse su **Visualizzatore eventi (locale)**. Scegliere **Connetti a un altro computer**, quindi immettere le informazioni necessarie nella finestra di dialogo **Selezione computer**.  
  
5. Facoltativamente, per visualizzare solo gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], scegliere **Filtro** dal menu **Visualizza**. Selezionare **MSSQLSERVER** nell'elenco **Origine evento**. Per visualizzare solo gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent selezionare invece **SQLSERVERAGENT** nell'elenco **Origine evento** .  
  
6. Per visualizzare ulteriori informazioni su un evento, fare doppio clic sull'evento stesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare il log degli errori di SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
