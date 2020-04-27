---
title: Gli hint di tabella nelle definizioni delle viste indicizzate vengono ignorati nella modalità di compatibilità 80 e non sono consentiti in modalità 90 o versioni successive | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091810"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>Gli hint di tabella contenuti nelle definizioni delle viste indicizzate vengono ignorati in modalità di compatibilità 80 e non sono consentiti in modalità di compatibilità 90 o successiva
  In modalità di compatibilità 90 o successiva, gli hint di tabella non sono consentiti nelle definizioni delle viste indicizzate. Per ulteriori informazioni, vedere gli argomenti seguenti nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: "Progettazione di viste indicizzate", "Creazione di viste indicizzate" e "Hint per la query ([!INCLUDE[tsql](../../includes/tsql-md.md)])".  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Gli hint di tabella devono essere rimossi dalle definizioni delle viste indicizzate. Indipendentemente dalla modalità di compatibilità utilizzata, si consiglia di testare l'applicazione per verificare la corretta esecuzione delle operazioni di creazione, aggiornamento e accesso alle viste indicizzate, inclusa l'associazione di query a viste indicizzate.  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
