---
title: Credenziali Oracle per l'esecuzione di script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca3f76c49b950f6830c4d60f011bbdb158055179
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796093"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  Per eseguire lo script di registrazione supplementare di Oracle da CDC Designer Console, vengono richieste le credenziali dell'utente Oracle che esegue lo script. Per eseguire questo script, l'utente Oracle deve disporre dell'autorizzazione ALTER TABLE per tutte le tabelle da acquisire e dell'autorizzazione SELECT per la vista DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Elenco attività  
 Immettere quanto segue nella finestra di dialogo:  
  
 **Autenticazione**  
  
 Selezionare una delle opzioni seguenti:  
  
-   **L'autenticazione di Windows**: Selezionare questa opzione per utilizzare le credenziali di dominio Windows correnti. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.  
  
-   **Oracle Authentication**: Se si seleziona questa opzione, è necessario digitare il **nome utente** e **Password** per l'utente nel database Oracle di origine si è connessi.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di gestione di un'istanza di CDC](manage-a-cdc-instance.md)   
 [Rivedere e generare script di registrazione supplementare](review-and-generate-supplemental-logging-scripts.md)  
  
  
