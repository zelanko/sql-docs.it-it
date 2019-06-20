---
title: osql non supporta più I comandi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ce7bfa0bbeec5c5ca83b7139f0ff28e3994021d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093721"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql non supporta più comandi
  Il **osql** utilità non supporta la **ED** e **!!** .  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere i riferimenti per il **ED** e **!!** dagli script.  
  
 Se si desidera utilizzare il **ED** e **!!** i comandi, usare il **sqlcmd** utilità anziché **osql**.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
