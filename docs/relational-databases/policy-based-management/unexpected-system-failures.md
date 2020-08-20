---
description: Errori di sistema imprevisti
title: Errori di sistema imprevisti | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6b1a4f991bf531b109fd76665be43274c68f2a88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490679"
---
# <a name="unexpected-system-failures"></a>Errori di sistema imprevisti
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questa regola consente di controllare l'evento SYSTEM 6008 nel registro eventi del computer. Questo evento indica un arresto del sistema imprevisto. Il sistema potrebbe essere instabile e non fornire la stabilità e l'integrità necessarie per ospitare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Determinare immediatamente la causa dei riavvii imprevisti del server oppure spostare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un altro computer.  
  
  
