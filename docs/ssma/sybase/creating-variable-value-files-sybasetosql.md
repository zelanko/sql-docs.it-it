---
title: Creazione di file di valore della variabile (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7afced10f0be71310edc4b42ea0158ca996f3aa3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63069666"
---
# <a name="creating-variable-value-files-sybasetosql"></a>Creazione di file di valori di variabile (SybaseToSQL)
File di valore variabile è un file XML che includono i valori dei parametri dei comandi, ad esempio, il nome del server di origine o di destinazione che cambiano spesso dalla migrazione di un server a un altro. Quando si verifica un numero elevato di migrazioni del database, più file variabili per archiviare il valore di ogni server di origine verranno creati e fa riferimento a un file di script master con il **- v** passare alla riga di comando. Ciò consente la gestione dei valori statici in alcuni file di script con i valori delle variabili in più file di variabili.  
  
> [!NOTE]  
> 1.  I nomi delle variabili sono il prefisso e suffisso con un simbolo di dollaro $. Se le variabili non sono assegnate un valore nel file di valore della variabile, si verificherà un errore durante l'analisi del file script risultante in blocco il processo di esecuzione della console.  
> 2.  Il carattere di escape per **$** viene **$$** . Se il valore di un valore statico o variabile di un parametro contiene **$** simbolo (dollaro), quindi **$$** deve essere specificata di considerarlo come un carattere anziché una variabile.  
> 3.  Ai fini delle manutenibilità, le variabili possono essere dichiarate all'interno di `'variable-group'` elementi per la separazione logica dell'utente definite variabili.  Utilizzo di questo elemento non è obbligatorio.  
  
**Esempi:**  
  
**Esempio 1:**  
  
```xml  
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
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
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
  
## <a name="variable-value-file-validation"></a>Convalida del valore della variabile del File  
L'utente può facilmente convalidare il file di valore della variabile in base al file di definizione dello schema **ConsoleScriptVariablesSchema.xsd** disponibile nella cartella "Schemi".  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [creazione di file di connessione del Server &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione dei file Server (Sybase)](https://msdn.microsoft.com/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  
