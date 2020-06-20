---
title: Rimuovere le operazioni DDL sulle tabelle inserite ed eliminate all'interno di trigger DML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- data definition language [SQL Server]
- DDL statements [SQL Server]
- DML triggers, removing DDL operations
ms.assetid: e49ba7d5-787f-4052-b985-b699195d982b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 61f7ab78b5ab6251b7f27401d36423ec27141c4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041840"
---
# <a name="remove-ddl-operations-on-the-inserted-and-deleted-tables-inside-dml-triggers"></a>Rimuovere le istruzioni DDL eseguite su tabelle inserite ed eliminate all'interno di trigger DML
  Non è possibile eseguire istruzioni DDL (Data Definition Language), ad esempio CREATE INDEX, su tabelle inserite ed eliminate all'interno di trigger DML. Alcune istruzioni DDL sulle tabelle inserite ed eliminate sono consentite nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere "Utilizzo delle tabelle inserted e deleted" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere le istruzioni DLL eseguite nelle tabelle inserite ed eliminate all'interno di trigger DML.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
