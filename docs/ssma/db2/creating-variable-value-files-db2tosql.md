---
title: Creazione di file di valore della variabile (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cf62d09de1180687598d817ff9199d7098008829
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299136"
---
# <a name="creating-variable-value-files-db2tosql"></a>Creazione di file di valore della variabile (DB2ToSQL)
File di valore variabile è un file XML che includono i valori dei parametri dei comandi, ad esempio, il nome del server di origine o di destinazione che cambiano spesso dalla migrazione di un server a un altro. Quando si verifica un numero elevato di migrazioni del database, più file variabili per archiviare il valore di ogni server di origine verranno creati e fa riferimento a un file di script master con il **- v** passare alla riga di comando. Ciò consente la gestione dei valori statici in alcuni file di script con i valori delle variabili in più file di variabili.  
  
> [!NOTE]  
> 1.  I nomi delle variabili sono il prefisso e suffisso con un simbolo di dollaro $. Se le variabili non sono assegnate un valore nel file di valore della variabile, si verificherà un errore durante l'analisi del file script risultante in blocco il processo di esecuzione della console.  
> 2.  Il carattere di escape per **$** viene **$$**. Se il valore di un valore statico o variabile di un parametro contiene **$** simbolo (dollaro), quindi **$$** deve essere specificata di considerarlo come un carattere anziché una variabile.  
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
Il passaggio successivo in costi operativi console consiste [creazione di file di connessione del Server &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione dei file di connessione del server](../oracle/creating-the-server-connection-files-oracletosql.md)  
  
