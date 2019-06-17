---
title: Creazione di file di valore della variabile (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 73919295dbd53cbaaca3847d5be119e5fe2d0bb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183095"
---
# <a name="creating-variable-value-files-mysqltosql"></a>Creazione di file di valori di variabile (MySQLToSQL)
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
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
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
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
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
L'utente può facilmente convalidare il file di valore della variabile in base al file di definizione dello schema **'ConsoleScriptVariablesSchema.xsd'** disponibile nella cartella "Schemi".  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [creazione di file di connessione del Server &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di file di connessione del Server (MySQL)](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
