---
title: Nome di named pipe non valido può bloccare l'aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad261d8d7680be7111e79a1b7a7f3291c2139308
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582814"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Un nome di named pipe non valido può bloccare l'aggiornamento
  L'aggiornamento non riesce se il protocollo Named Pipes non è configurato correttamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Durante l'aggiornamento, viene avviato il programma di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] istanza con supporto della memoria condivisa, una named pipe che accetta solo connessioni locali. Se il nome di pipe specificato nel server non è vuoto, deve iniziare con la stringa "\\\\. \pipe\\" sia valido. Se il nome non è valido, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non verrà avviato e l'installazione non verrà completata.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Usare la  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilità di rete** per attribuire un nome valido alla named pipe, quindi eseguire il programma di installazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
