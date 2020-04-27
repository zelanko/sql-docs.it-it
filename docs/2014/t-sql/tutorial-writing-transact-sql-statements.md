---
title: 'Esercitazione: Scrittura di istruzioni Transact-SQL | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 67e09713fdec72313bde6ba81e1cc169467fda0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211191"
---
# <a name="tutorial-writing-transact-sql-statements"></a>Esercitazione: Scrittura di istruzioni Transact-SQL
  L'esercitazione per la scrittura di istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] è destinata agli utenti che non hanno familiarità con la scrittura delle istruzioni SQL e consentirà ai nuovi utenti di esaminare alcune istruzioni di base per creare tabelle e inserire i dati. Ai fini di questa esercitazione viene utilizzato [!INCLUDE[tsql](../includes/tsql-md.md)], l'implementazione [!INCLUDE[msCoName](../includes/msconame-md.md)] dello standard SQL. Questa esercitazione costituisce una breve introduzione al linguaggio [!INCLUDE[tsql](../includes/tsql-md.md)] e non rappresenta un'alternativa a un corso su [!INCLUDE[tsql](../includes/tsql-md.md)] . Le istruzioni incluse in questa esercitazione sono intenzionalmente semplici e non sono progettate per illustrare la complessità di un tipico database di produzione.  
  
> [!NOTE]  
>  Per gli utenti che non hanno familiarità con i database risulta in genere più semplice utilizzare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] anziché tramite la scrittura di istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
## <a name="finding-more-information"></a>Per ulteriori informazioni  
 Per altre informazioni su un'istruzione specifica, cercare il nome dell'istruzione nella documentazione online di SQL Server oppure usare il sommario per individuare i 1.800 elementi del linguaggio elencati in ordine alfabetico in [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference). È inoltre possibile trovare informazioni eseguendo una ricerca per parole chiave correlate all'oggetto di proprio interesse. Se ad esempio si vogliono informazioni su come restituire una parte di una data, come il mese, cercare **dates [SQL Server]** nell'indice e selezionare **dateparts**. Si accede così all'argomento [DATEPART &#40;Transact-SQL&#41;](/sql/t-sql/functions/datepart-transact-sql). Oppure, per trovare informazioni sull'uso delle stringhe, cercare ad esempio **funzioni stringa**. Si accede così all'argomento [Funzioni per i valori stringa &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql).  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione vengono illustrate le procedure per la creazione di un database e di una tabella, per l'inserimento di dati in quest'ultima e quindi per la lettura, l'aggiornamento e l'eliminazione dei dati, nonché per l'eliminazione della tabella. Verranno create viste e stored procedure e verrà configurato un utente per il database e i dati.  
  
 L'esercitazione è suddivisa in tre lezioni:  
  
 [Lezione 1: Creazione di oggetti di database](lesson-1-creating-database-objects.md)  
 In questa lezione si procederà alla creazione di un database, alla creazione di una tabella, all'inserimento in quest'ultima dei dati che verranno quindi aggiornati e letti.  
  
 [Lezione 2: Configurazione delle autorizzazioni per gli oggetti di database](lesson-2-configuring-permissions-on-database-objects.md)  
 In questa lezione si procederà alla creazione di un account di accesso e un utente. Verranno inoltre create una vista e una stored procedure e si concederanno all'utente le autorizzazioni necessarie per l'esecuzione della stored procedure.  
  
 [Lezione 3: Eliminazione di oggetti di database](lesson-3-1-deleting-database-objects.md)  
 In questa lezione si procederà alla rimozione dell'accesso ai dati, all'eliminazione di questi da una tabella che verrà a sua volta eliminata e quindi all'eliminazione del database.  
  
## <a name="requirements"></a>Requisiti  
 Per completare questa esercitazione non è necessario conoscere il linguaggio SQL. È tuttavia consigliabile conoscere i concetti di base correlati ai database, ad esempio le tabelle. Durante l'esercitazione verranno creati un database e un utente di Windows. Per queste attività è necessario disporre di un livello elevato di autorizzazione. È pertanto consigliabile accedere al computer come amministratore.  
  
 È necessario che nel sistema siano installati i componenti seguenti:  
  
-   Qualsiasi edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o Management Studio Express.  
  
-   Internet Explorer 6 o versione successiva.  
  
> [!NOTE]  
>  Quando si esaminano le esercitazioni, è consigliabile aggiungere i pulsanti **Avanti** e **indietro** alla barra degli strumenti del Visualizzatore di documenti.  
  
  
