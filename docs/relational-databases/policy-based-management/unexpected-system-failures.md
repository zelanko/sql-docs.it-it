---
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
ms.openlocfilehash: 84fe7ae204c14a0ecaebb3141d4f08175bfee793
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727274"
---
# <a name="unexpected-system-failures"></a>Errori di sistema imprevisti
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questa regola consente di controllare l'evento SYSTEM 6008 nel registro eventi del computer. Questo evento indica un arresto del sistema imprevisto. Il sistema potrebbe essere instabile e non fornire la stabilità e l'integrità necessarie per ospitare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Determinare immediatamente la causa dei riavvii imprevisti del server oppure spostare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un altro computer.  
  
  
