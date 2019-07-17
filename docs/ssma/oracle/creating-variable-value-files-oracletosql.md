---
title: Creazione di file di valore della variabile (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Variable Value File Creation
- Variable Value File, Variable Value File Validation
ms.assetid: f583d81a-8e34-41b1-8100-ee3a6a82213b
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 87db0ebd006e2ca87ddc4744a4bbcd396a827712
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266118"
---
# <a name="creating-variable-value-files-oracletosql"></a>Creazione di file di valori di variabile (OracleToSQL)
File di valore variabile è un file XML che includono i valori dei parametri dei comandi, ad esempio, il nome del server di origine o di destinazione che cambiano spesso dalla migrazione di un server a un altro. Quando si verifica un numero elevato di migrazioni del database, più file variabili per archiviare il valore di ogni server di origine verranno creati e fa riferimento a un file di script master con il **- v** passare alla riga di comando. Ciò consente la gestione dei valori statici in alcuni file di script con i valori delle variabili in più file di variabili.  
  
> [!NOTE]  
> 1.  I nomi delle variabili sono il prefisso e suffisso con un simbolo di dollaro $. Se le variabili non sono assegnate un valore nel file di valore della variabile, si verificherà un errore durante l'analisi del file script risultante in blocco il processo di esecuzione della console.  
> 2.  Il carattere di escape per **$** viene **$$** . Se il valore di un valore statico o variabile di un parametro contiene **$** simbolo (dollaro), quindi **$$** deve essere specificata di considerarlo come un carattere anziché una variabile.  
> 3.  Ai fini delle manutenibilità, le variabili possono essere dichiarate all'interno di `'variable-group'` elementi per la separazione logica dell'utente definite variabili.  Utilizzo di questo elemento non è obbligatorio.  
  
**Esempi:**  
  
**Esempio 1:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**Esempio 2:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [creazione di file di connessione del Server &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione dei file Server (Oracle)](https://msdn.microsoft.com/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  
