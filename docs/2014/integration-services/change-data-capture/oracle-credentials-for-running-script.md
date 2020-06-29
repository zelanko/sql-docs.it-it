---
title: Credenziali Oracle per l'esecuzione di script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 683b313e5b1065c3709c4637ddf968641612cc0b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438558"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  Per eseguire lo script di registrazione supplementare di Oracle da CDC Designer Console, vengono richieste le credenziali dell'utente Oracle che esegue lo script. Per eseguire questo script, l'utente Oracle deve disporre dell'autorizzazione ALTER TABLE per tutte le tabelle da acquisire e dell'autorizzazione SELECT per la vista DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Elenco attività  
 Immettere quanto segue nella finestra di dialogo:  
  
 **autenticazione**  
  
 Selezionare uno degli elementi seguenti:  
  
-   **Windows Authentication**: selezionare questa opzione per utilizzare le credenziali del dominio Windows correnti. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.  
  
-   **Oracle Authentication**: se si seleziona questa opzione, è necessario digitare il **nome utente** e la **password** dell'utente nel database Oracle di origine a cui si effettua la connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [Rivedere e generare script di registrazione supplementare](review-and-generate-supplemental-logging-scripts.md)  
  
  
