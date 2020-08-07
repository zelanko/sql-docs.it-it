---
title: Creazione di file di valori di variabile (OracleToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 763785b09adf1a562d497d4c1b448ec03d502bfc
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934928"
---
# <a name="creating-variable-value-files-oracletosql"></a>Creazione di file di valori di variabile (OracleToSQL)
Il file di valori di variabile è un file XML che include i valori dei parametri, ad esempio, il nome del server di origine o di destinazione che cambia di frequente da una migrazione del server a un'altra. Quando si verifica un numero elevato di migrazioni di database, vengono creati più file di variabili per l'archiviazione del valore di ogni server di origine a cui viene fatto riferimento in un file di script Master con l'opzione **-v** nella riga di comando. Questo consente di mantenere i valori statici in pochi file di script con i valori delle variabili in più file variabili.  
  
> [!NOTE]  
> 1.  I nomi delle variabili hanno il prefisso e il suffisso è un simbolo di $ (dollaro). Se alle variabili non viene assegnato un valore nel file di valori di variabile, si verificherà un errore durante l'analisi del file di script, con conseguente blocco del processo di esecuzione della console.  
> 2.  Il carattere di escape per **$** è **$$** . Se il valore di una variabile o di un valore statico di un parametro contiene il **$** simbolo (dollaro), **$$** è necessario specificare per considerarlo come un carattere anziché come variabile.  
> 3.  Ai fini della gestibilità, le variabili possono essere dichiarate all'interno di `'variable-group'` elementi per la separazione logica delle variabili definite dall'utente.  L'utilizzo di questo elemento non è obbligatorio.  
  
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
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo per la gestione della console consiste nel [creare i file di connessione del Server &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Creazione dei file server (Oracle)](https://msdn.microsoft.com/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  
