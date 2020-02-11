---
title: Connetti al server (pagina Parametri aggiuntivi per la connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e92fbb8bc29aed54e43925a0670d9a365388df62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808672"
---
# <a name="connect-to-server-additional-connection-parameters-page"></a>Connetti al server (pagina Parametri aggiuntivi per la connessione)
  Nella finestra di dialogo di **connessione** al server di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] sono disponibili le opzioni relative ai valori della stringa di connessione più comuni. Usare la pagina **Parametri aggiuntivi per la connessione** per aggiungere più parametri di connessione alla stringa di connessione.  
  
-   Qualsiasi parametro di connessione ODBC può costituire un parametro aggiuntivo per la connessione.  
  
-   I parametri aggiuntivi per la connessione devono essere aggiunti nel formato **;parametro1=valore1;parametro2=valore2**.  
  
-   I parametri aggiunti usando la pagina **Parametri aggiuntivi per la connessione** vengono aggiunti ai parametri selezionati usando le opzioni della finestra di dialogo **Connetti al server** .  
  
-   L'ultima istanza di ogni parametro specificato sostituisce eventuali istanze precedenti del parametro stesso. I parametri aggiunti tramite la pagina **Parametri aggiuntivi per la connessione** seguono e sostituiscono i parametri specificati nelle schede **Account di accesso** o **Proprietà connessione** . Se, ad esempio, nella scheda **Account di accesso** è specificato **SERVER1** come **Nome server**e la pagina **Parametri aggiuntivi per la connessione** contiene **;SERVER=SERVER2**, verrà stabilita la connessione a **SERVER2**.  
  
-   I parametri aggiunti usando la pagina **Parametri aggiuntivi per la connessione** vengono sempre passati come testo normale.  
  
    > [!IMPORTANT]  
    >  Non includere credenziali di accesso e password nella pagina **Parametri aggiuntivi per la connessione** , non verranno crittografate quando vengono passate in rete. Usare invece la scheda **Account di accesso** .  
  
## <a name="task-list"></a>Elenco attività  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>Per visualizzare la pagina Parametri aggiuntivi per la connessione  
  
1.  In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]scegliere **Connessione** dal menu **Query**, quindi fare clic su **Connetti**.  
  
2.  Nella finestra di dialogo **Connetti al server** fare clic su **Opzioni**e quindi sulla scheda **Parametri aggiuntivi per la connessione** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="example-a-connecting-to-the-database-engine"></a>Esempio 1: Connessione al Motore di database  
 Per connettersi al database [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] in un server denominato ACCOUNTING, immettere quanto indicato di seguito nella pagina **Parametri aggiuntivi per la connessione** :  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>Esempio B: Connessione ad Analysis Services  
 Per connettersi ad Analysis Services e fare in modo che tutte le partizioni in attesa di notifiche vengano sottoposte a query in tempo reale (ignorando la memorizzazione nella cache) e per impostare il valore di timeout del writeback su 5, immettere quanto indicato di seguito nella pagina **Parametri aggiuntivi per la connessione** :  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
