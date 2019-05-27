---
title: Hint di tabella nella vista definizioni vengono ignorate in modalità di compatibilità 80 e non sono consentite nella modalità 90 o versioni successive indicizzata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69a6bae06b1cb5d7a727ff2582f10bccf1e21ca8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091810"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>Gli hint di tabella contenuti nelle definizioni delle viste indicizzate vengono ignorati in modalità di compatibilità 80 e non sono consentiti in modalità di compatibilità 90 o successiva
  In modalità di compatibilità 90 o successiva, gli hint di tabella non sono consentiti nelle definizioni delle viste indicizzate. Per altre informazioni, vedere gli argomenti seguenti nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione in linea: "Progettazione di viste indicizzate", "Creazione di viste indicizzate," e "hint per la Query ([!INCLUDE[tsql](../../includes/tsql-md.md)])."  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Gli hint di tabella devono essere rimossi dalle definizioni delle viste indicizzate. Indipendentemente dalla modalità di compatibilità utilizzata, si consiglia di testare l'applicazione per verificare la corretta esecuzione delle operazioni di creazione, aggiornamento e accesso alle viste indicizzate, inclusa l'associazione di query a viste indicizzate.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
