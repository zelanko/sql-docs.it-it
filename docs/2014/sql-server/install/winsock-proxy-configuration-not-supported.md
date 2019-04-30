---
title: Configurazione Winsock Proxy non supportata | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Winsock proxy configuration [SQL Server]
ms.assetid: abf71f7b-8bd7-49d2-92f7-9ddf72924d8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e9f73710f1cdb13477736d3b7496fb26b76f90e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184492"
---
# <a name="winsock-proxy-configuration-not-supported"></a>Configurazione proxy WinSock non supportata
  Il proxy Winsock non può essere configurato utilizzando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] strumenti.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Impossibile configurare componenti WinSock con gli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Utilizzare Microsoft Internet Security and Acceleration (ISA) Server per pubblicare un computer. Per informazioni sulla configurazione del proxy WinSock, vedere la documentazione del server proxy.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
