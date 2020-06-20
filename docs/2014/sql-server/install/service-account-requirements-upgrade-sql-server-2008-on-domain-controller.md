---
title: Requisiti dell'account del servizio per l'aggiornamento a SQL Server 2008 in un controller di dominio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0680e09548e38760f6ac317fec63152486a4e5fb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036507"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>Requisiti dell'account del servizio per l'aggiornamento a SQL Server 2008 in un controller di dominio
  È stata rilevata un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in un servizio di rete o in un account del servizio locale in un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] controller di dominio. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installato in un controller di dominio [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], non è possibile eseguire i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i privilegi dell'account Servizio locale o Servizio di rete.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Assicurarsi che tutti gli account del servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siano assegnati ad account Dominio o Sistema locale. Se questa modifica non viene eseguita prima dell'aggiornamento, l'installazione si bloccherà. Fanno eccezione i servizi writer SQL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Active Directory Helper degli account del servizio, per i quali l'utilizzo dell'account servizio di rete è specificato a livello di codice e non può essere modificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
