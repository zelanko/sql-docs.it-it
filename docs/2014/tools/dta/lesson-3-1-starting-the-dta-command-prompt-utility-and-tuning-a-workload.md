---
title: Avvio dell'utilità del prompt dei comandi dta e ottimizzazione di un carico di lavoro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf882bc731c8e435de808092e990b35ad23ce57e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110161"
---
# <a name="starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>Avvio dell'utilità del prompt dei comandi dta e ottimizzazione di un carico di lavoro
  In questa attività vengono illustrate le procedure per avviare l'utilità **dta**, visualizzarne la Guida e quindi usare l'utilità dal prompt dei comandi per ottimizzare un carico di lavoro. Viene usato il carico di lavoro MyScript.sql creato per l'esercitazione sull'interfaccia utente grafica di Ottimizzazione guidata motore di database [Ottimizzazione di un carico di lavoro](lesson-1-1-tuning-a-workload.md).  
  
 In questa esercitazione viene utilizzato il database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Per motivi di sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database di esempio, vedere [Installazione degli esempi e dei database di esempio di SQL Server](http://sqlserversamples.codeplex.com).  
  
 Le attività seguenti consentono di aprire un prompt dei comandi, avviare l'utilità della riga di comando **dta** , visualizzare la Guida relativa alla sintassi e ottimizzare un carico di lavoro semplice, ovvero MyScript.sql, creato in [Ottimizzazione di un carico di lavoro](lesson-1-1-tuning-a-workload.md).  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>Per avviare l'utilità del prompt dei comandi dta e visualizzare la Guida  
  
1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi**, **Accessori**e quindi **Prompt dei comandi**.  
  
2.  Al prompt dei comandi digitare quanto segue e premere INVIO:  
  
    ```  
    dta -? | more  
    ```  
  
     La sezione `| more` di questo comando è facoltativa. Tuttavia utilizzandola è possibile scorrere le pagine della Guida dell'utilità relative alla sintassi. Premere INVIO per visualizzare il testo della Guida riga per riga oppure premere la BARRA SPAZIATRICE per scorrere le pagine.  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>Per ottimizzare un carico di lavoro semplice utilizzando l'utilità del prompt dei comandi dta  
  
1.  Al prompt dei comandi, passare alla directory contenente il file MyScript.sql.  
  
2.  Al prompt dei comandi, digitare quanto segue e premere INVIO per eseguire il comando e avviare la sessione di ottimizzazione (si noti che l'utilità distingue tra maiuscole e minuscole quando viene eseguita l'analisi dei comandi):  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
     dove `-S` indica il nome del server e l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è installato il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . L'impostazione `-E` indica l'utilizzo di una connessione trusted all'istanza che risulta appropriata nel caso di una connessione con un account di dominio di Windows. L'impostazione `-D` specifica il database da ottimizzare, `-if` il file del carico di lavoro, `-s` il nome della sessione, `-of` il file sul quale verrà creato lo script delle indicazioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e `-ox` il file sul quale verranno scritte le indicazioni in formato XML. Gli ultimi tre parametri definiscono le opzioni di ottimizzazione nel modo seguente: `-fa IDX_IV` indica che in Ottimizzazione guidata motore di database devono essere aggiunti solo gli indici (cluster e non cluster) e le viste indicizzate; `-fp NONE` indica che durante l'analisi non devono essere considerate le strategie di partizionamento e `-fk NONE` indica che quando vengono generate le indicazioni in Ottimizzazione guidata motore di database non devono essere mantenute nel database le strutture di progettazione fisica esistenti.  
  
3.  Al termine dell'ottimizzazione del carico di lavoro, in Ottimizzazione guidata motore di database viene visualizzato un messaggio che indica che la sessione di ottimizzazione è stata completata correttamente. È possibile visualizzare i risultati dell'ottimizzazione utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per aprire i file MySession2OutputScript.sql e MySession2Output.xml. In alternativa è possibile aprire la sessione di ottimizzazione MySession2 nell'interfaccia utente grafica di Ottimizzazione guidata motore di database e visualizzare le indicazioni e i report come descritto in [Visualizzazione delle indicazioni di ottimizzazione](lesson-1-2-viewing-tuning-recommendations.md) e [Visualizzazione dei report di ottimizzazione](lesson-1-3-viewing-tuning-reports.md).  
  
## <a name="summary"></a>Riepilogo  
 In questo modo è stata completata l'ottimizzazione di un carico di lavoro semplice dal prompt dei comandi tramite l'utilità **dta** . Questo strumento offre numerose altre opzioni di ottimizzazione. Per altre informazioni, consultare la Guida (**dta -?**) e l'argomento [Utilità dta](dta-utility.md) .  
  
## <a name="after-you-finish-this-tutorial"></a>Al termine di questa esercitazione  
 Al termine di questa esercitazione, per ulteriori informazioni sullo strumento Ottimizzazione guidata motore di database, è possibile consultare gli argomenti seguenti:  
  
-   [Ottimizzazione guidata motore di database](../../relational-databases/performance/database-engine-tuning-advisor.md) per le descrizioni sull'uso di questo strumento in determinate attività.  
  
-   [Utilità dta](dta-utility.md) per materiale di riferimento sull'utilità del prompt dei comandi e sul file XML facoltativo disponibile per usare l'utilità.  
  
 Per tornare all'inizio dell'esercitazione, vedere [esercitazione: Ottimizzazione guidata motore di database](tutorial-database-engine-tuning-advisor.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni del motore di database](../../relational-databases/database-engine-tutorials.md)  
  
  
