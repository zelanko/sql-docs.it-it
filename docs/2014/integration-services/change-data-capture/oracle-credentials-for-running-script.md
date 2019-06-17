---
title: Credenziali Oracle per l'esecuzione di script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12de97bf147ccb61cde5f82e2fa31782404071e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771112"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  Per eseguire lo script di registrazione supplementare di Oracle da CDC Designer Console, vengono richieste le credenziali dell'utente Oracle che esegue lo script. Per eseguire questo script, l'utente Oracle deve disporre dell'autorizzazione ALTER TABLE per tutte le tabelle da acquisire e dell'autorizzazione SELECT per la vista DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Elenco attività  
 Immettere quanto segue nella finestra di dialogo:  
  
 **Autenticazione**  
  
 Selezionare una delle opzioni seguenti:  
  
-   **Windows Authentication**: selezionare questa opzione per utilizzare le credenziali del dominio Windows correnti. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.  
  
-   **Oracle Authentication**: se si seleziona questa opzione, è necessario digitare il **nome utente** e la **password** dell'utente nel database Oracle di origine a cui si effettua la connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di gestione di un'istanza di CDC](manage-a-cdc-instance.md)   
 [Rivedere e generare script di registrazione supplementare](review-and-generate-supplemental-logging-scripts.md)  
  
  
