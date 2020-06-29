---
title: Eseguire il mapping dei parametri di query a variabili in un'attività Esegui SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameterized SQL commands [Integration Services]
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- Execute SQL task [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 6a164349-dfcf-4995-80bc-d4e7aee52a83
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b2e105e2ccccce912965cbfc0662a380ea1a6264
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440268"
---
# <a name="map-query-parameters-to-variables-in-an-execute-sql-task"></a>Mapping di parametri di query a variabili in un'attività Esegui SQL

  In questo argomento viene descritto come utilizzare un'istruzione SQL con parametri nell'attività Esegui SQL e come creare mapping tra variabili e parametri dell'istruzione SQL.  
  
 Per sapere di più sull'attività Esegui SQL, sugli indicatori di parametro e sui nomi dei parametri usati con i diversi tipi di connessione, vedere [Attività Esegui SQL](control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Per eseguire il mapping di un parametro di query a una variabile  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che si desidera utilizzare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Se il pacchetto non include già un'attività Esegui SQL, aggiungerne una al flusso di controllo del pacchetto. Per altre informazioni, vedere [aggiungere o eliminare un'attività o un contenitore in un flusso di controllo](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  Fare doppio clic sull'attività Esegui SQL.  
  
6.  Specificare un comando SQL con parametri in uno dei modi seguenti:  
  
    -   Usare l'input diretto e digitare il comando SQL nella proprietà SQLStatement.  
  
    -   Usare l'input diretto, fare clic su **Compila query**, quindi creare un comando SQL usando gli strumenti grafici disponibili in Generatore query.  
  
    -   Utilizzare una connessione file e quindi fare riferimento al file che contiene il comando SQL.  
  
    -   Utilizzare una variabile e quindi fare riferimento alla variabile che contiene il comando SQL.  
  
     I marcatori di parametro che è possibile utilizzare nelle istruzioni SQL con parametri dipendono dal tipo di connessione utilizzato dall'attività Esegui SQL.  
  
    |Tipo di connessione|Marcatore di parametro|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET e SQLMOBILE|@\<parameter name>|  
    |ODBC|?|  
    |EXCEL e OLE DB|?|  
  
     Nella tabella seguente sono elencati esempi di comandi SELECT per tipo di gestione connessione. I parametri specificano i valori del filtro per la clausola WHERE. Negli esempi l'istruzione SELECT viene usata per recuperare dalla tabella **Product** del database [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] i prodotti con **ProductID** compreso tra i valori specificati da due parametri.  
  
    |Tipo di connessione|Sintassi dell'istruzione SELECT|  
    |---------------------|-------------------|  
    |EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
     Per esempi di utilizzo di parametri con stored procedure, vedere [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
7.  Fare clic su **Mapping parametri**.  
  
8.  Per aggiungere un mapping parametri, fare clic su **Aggiungi**.  
  
9. Specificare un nome nella casella **Nome parametro** .  
  
     I nomi dei parametri utilizzati dipendono dal tipo di connessione utilizzato dall'attività Esegui SQL.  
  
    |Tipo di connessione|Nome parametro|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, ...|  
    |ADO.NET e SQLMOBILE|@\<parameter name>|  
    |ODBC|1, 2, 3, ...|  
    |EXCEL e OLE DB|0, 1, 2, 3, ...|  
  
10. Selezionare una variabile nell'elenco **Nome variabile** . Per altre informazioni, vedere [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
11. Nell'elenco **Direzione** specificare se il parametro è un input, un output o un valore restituito.  
  
12. Nell'elenco **Tipo di dati** impostare il tipo di dati del parametro.  
  
    > [!IMPORTANT]  
    >  Il tipo di dati del parametro deve essere compatibile con quello della variabile.  
  
13. Ripetere i passaggi da 8 a 11 per ogni parametro nell'istruzione SQL.  
  
    > [!IMPORTANT]  
    >  I mapping dei parametri devono essere specificati nello stesso ordine con cui compaiono i parametri nell'istruzione SQL.  
  
14. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Esegui SQL](control-flow/execute-sql-task.md)   
 [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
  
