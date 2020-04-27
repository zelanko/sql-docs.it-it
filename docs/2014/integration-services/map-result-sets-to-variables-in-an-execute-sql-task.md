---
title: Mapping di set di risultati a variabili in un'attività Esegui SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 995afe55c1cd1b7d925c9267ba5dfa3aed038358
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057762"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>Mapping di set di risultati a variabili in un'attività Esegui SQL
  Questo argomento descrive la procedura per il mapping di un set di risultati a una variabile in un'attività Esegui SQL. Se su un set di risultati viene eseguito il mapping a una variabile, sarà disponibile anche per altri elementi nel pacchetto. Si consideri ad esempio un'attività Script contenente uno script in grado di leggere la variabile e quindi utilizzare i valori del set di risultati oppure un'origine XML in grado di utilizzare il set di risultati archiviato in una variabile. Se viene generato da un pacchetto padre, il set di risultati potrà essere reso disponibile a un pacchetto figlio chiamato da un'attività Esegui pacchetto mappando tale set di risultati a una variabile nel pacchetto padre e quindi creando nel pacchetto figlio una configurazione Variabile pacchetto padre, per l'archiviazione del valore della variabile padre.  
  
 Per le descrizioni dei diversi tipi di set di risultati e i tipi di dati della variabile di cui è possibile eseguire il mapping ai set di risultati, vedere [Set di risultati nell'attività Esegui SQL](control-flow/execute-sql-task.md).  
  
### <a name="to-map-a-result-set-to-a-variable"></a>Per eseguire il mapping di un set di risultati a una variabile  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In **Esplora soluzioni**fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Se il pacchetto non include già un'attività Esegui SQL, aggiungerne una al flusso di controllo del pacchetto. Per altre informazioni, vedere [aggiungere o eliminare un'attività o un contenitore in un flusso di controllo](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  Fare doppio clic sull'attività Esegui SQL.  
  
6.  Nella pagina **Generale** della finestra di dialogo **Editor attività Esegui SQL** selezionare il tipo di set di risultati **Riga singola**, **Set dei risultati completo**o **XML** .  
  
     Per descrizioni dei diversi set di risultati, vedere [Set di risultati nell'attività Esegui SQL](result-sets-in-the-execute-sql-task.md)  
  
7.  Fare clic su **Set dei risultati**.  
  
8.  Per aggiungere un mapping del set dei risultati, fare clic su **Aggiungi**.  
  
9. Selezionare una variabile dall'elenco **Variables Name** (Nome variabili) o crearne una nuova. Per altre informazioni, vedere [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
     Per le descrizioni dei tipi di dati della variabile di cui è possibile eseguire il mapping ai diversi set di risultati, vedere [Set di risultati nell'attività Esegui SQL](result-sets-in-the-execute-sql-task.md).  
  
     Per informazioni su come eseguire il mapping di una variabile a una singola colonna e di più variabili a più colonne, vedere la sezione **Popolamento di una variabile con un set di risultati** in [Set di risultati nell'attività Esegui SQL](control-flow/execute-sql-task.md).  
  
10. Nell'elenco **Nome risultato** modificare il nome del set di risultati, se lo si desidera.  
  
     È in genere possibile utilizzare il nome della colonna come nome del set di risultati oppure utilizzare la posizione ordinale della colonna nell'elenco di colonne come set di risultati. La possibilità di utilizzare un nome di colonna come nome del set di risultati dipende dal provider per il quale l'attività è configurata. Non tutti i provider permettono l'uso di nomi di colonna.  
  
11. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedi anche  
 [Attività Esegui SQL](control-flow/execute-sql-task.md)   
 [Set di risultati nell'attività Esegui SQL](result-sets-in-the-execute-sql-task.md)   
 [Attività Esegui pacchetto](control-flow/execute-package-task.md)   
 [Configurazioni di pacchetti](../../2014/integration-services/package-configurations.md)   
 [Creazione di configurazioni di pacchetto](../../2014/integration-services/create-package-configurations.md)   
 [Usare i valori di variabili e parametri in un pacchetto figlio](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
  
