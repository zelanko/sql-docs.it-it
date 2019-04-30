---
title: Creazione di file di valore della variabile (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 00144c51e60b72fe043443d2a9c8d1d51a6cb8da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138833"
---
# <a name="creating-variable-value-files-accesstosql"></a>Creazione di file di valore della variabile (AccessToSQL)
Un File con valori di variabile è un file XML che includono i valori dei parametri dei comandi (ad esempio il nome di server di origine o destinazione) che cambiano di frequente tra le migrazioni di server. Quando si verifica un numero elevato di migrazioni del database, più file variabili per archiviare il valore di ogni server di origine vengono creati e fa riferimento a un file di script master con il **- v** passare alla riga di comando. Questo comportamento consente di mantenere valori statici in alcuni file di script con i valori delle variabili in più file di variabili.  
  
> [!NOTE]  
> -  I nomi delle variabili sono il prefisso e suffisso con un simbolo di dollaro $. Se una variabile non viene assegnata un valore nel file di valore della variabile, verificherà un errore durante l'analisi del file di script, risultante in blocco il processo di esecuzione della console.  
> -  Il carattere di escape per **$** viene **$$**. Se il valore di un valore statico o variabile di un parametro contiene un **$** simbolo (dollaro), quindi **$$** deve essere specificata di considerarlo come un carattere anziché una variabile.  
> -  Ai fini delle manutenibilità, le variabili possono essere dichiarate all'interno di `'variable-group'` elementi per la separazione logica delle variabili definite dall'utente.  Utilizzo di questo elemento non è obbligatorio.  
  
**Esempi:**  
  
**Esempio 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**Esempio 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>Convalida del valore della variabile del file  
L'utente può facilmente convalidare il file di valore della variabile in base al file di definizione dello schema **ConsoleScriptVariablesSchema.xsd** disponibile nella cartella "Schemi".  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [creazione di file di connessione del Server &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di file di connessione del Server (accesso)](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
