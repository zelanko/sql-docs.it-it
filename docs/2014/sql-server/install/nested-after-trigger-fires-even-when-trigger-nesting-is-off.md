---
title: I trigger AFTER nidificati viene attivata anche quando nidificazione dei trigger è OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, nested
- nested triggers option
- triggers [SQL Server], nested
ms.assetid: 94d72960-676e-40d9-81bc-08bffe778110
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0675c412d753a1ce60fa41c7ced40528b3c58f75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093832"
---
# <a name="nested-after-trigger-fires-even-when-trigger-nesting-is-off"></a>I trigger AFTER nidificati vengono attivati anche quando l'opzione relativa alla nidificazione dei trigger è disattivata
  È presente un trigger AFTER nidificato in un trigger INSTEAD OF definito su una o più tabelle. I trigger AFTER annidati possono essere attivati anche se l'opzione di configurazione del server `nested triggers` è impostata su 0.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Il primo trigger AFTER nidificato in un trigger INSTEAD OF viene attivato anche se l'opzione di configurazione del server `nested triggers` è impostata su 0. Tuttavia, con questa impostazione, i successivi trigger AFTER non vengono attivati.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Verificare se nelle proprie applicazioni sono presenti trigger nidificati per determinare se tali applicazioni sono comunque conformi alle regole business in uso, in relazione a questo nuovo comportamento quando l'opzione di configurazione del server `nested triggers` è impostata su 0, quindi apportare le modifiche eventualmente necessarie.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
