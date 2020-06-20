---
title: Il nome del named pipe non valido può bloccare l'aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: bacfd3d097d7cccb0a5780328c4db95dc5afc733
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059245"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Un nome di named pipe non valido può bloccare l'aggiornamento
  L'aggiornamento non riesce se il protocollo Named Pipes non è configurato correttamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Durante l'aggiornamento, il programma di installazione avvia l' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] istanza di con supporto Shared Memory, un named pipe che accetta solo connessioni locali. Se il nome della pipe specificato nel server non è vuoto, deve iniziare con la stringa " \\ \\ .\pipe \\ " per essere valido. Se il nome non è valido, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non verrà avviato e l'installazione non verrà completata.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Utilizzare l' ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilità di rete** per specificare un nome di pipe valido, quindi eseguire il programma di installazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
