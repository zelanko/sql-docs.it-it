---
title: Creazione di file di valori di variabile (MySQLToSQL) | Microsoft Docs
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
ms.openlocfilehash: be1530bdec1c1523a873dc93b1d70e6e72c880ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103020"
---
# <a name="creating-variable-value-files-mysqltosql"></a>Creazione di file di valori di variabile (MySQLToSQL)
Il file di valori di variabile è un file XML che include i valori dei parametri, ad esempio, il nome del server di origine o di destinazione che cambia di frequente da una migrazione del server a un'altra. Quando si verifica un numero elevato di migrazioni di database, vengono creati più file di variabili per l'archiviazione del valore di ogni server di origine a cui viene fatto riferimento in un file di script Master con l'opzione **-v** nella riga di comando. Questo consente di mantenere i valori statici in pochi file di script con i valori delle variabili in più file variabili.  
  
> [!NOTE]  
> 1.  I nomi delle variabili hanno il prefisso e il suffisso è un simbolo di $ (dollaro). Se alle variabili non viene assegnato un valore nel file di valori di variabile, si verificherà un errore durante l'analisi del file di script, con conseguente blocco del processo di esecuzione della console.  
> 2.  Il carattere di escape **$** per **$$** è. Se il valore di una variabile o di un valore statico di un **$** parametro contiene il simbolo (Dollaro **$$** ), è necessario specificare per considerarlo come un carattere anziché come variabile.  
> 3.  Ai fini della gestibilità, le variabili possono essere `'variable-group'` dichiarate all'interno di elementi per la separazione logica delle variabili definite dall'utente.  L'utilizzo di questo elemento non è obbligatorio.  
  
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
  
## <a name="variable-value-file-validation"></a>Convalida file di valori di variabile  
L'utente può convalidare facilmente il proprio file di valori di variabile rispetto al file di definizione dello schema **' ConsoleScriptVariablesSchema. xsd '** disponibile nella cartella ' schemi '.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo per la gestione della console consiste nel [creare i file di connessione del Server &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione dei file di connessione del server (MySQL)](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
