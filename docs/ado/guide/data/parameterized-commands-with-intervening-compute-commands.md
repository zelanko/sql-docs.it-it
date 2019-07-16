---
title: Comandi con i comandi di calcolo intermedi con parametri | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb6bc2b9f7e53caf28f44daf39815850940b9d3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924728"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Comandi con parametri con comandi COMPUTE intermedi
Una forma con parametri tipici comando APPEND disponga di una clausola che crea un elemento padre **Recordset** con un comando di query e un'altra clausola che crea un elemento figlio **Recordset** con un comando di query con parametri: vale a dire, un comando che contiene un segnaposto per il parametro (un punto interrogativo, "?"). Il data shaping risultante **Recordset** ha due livelli, in cui l'elemento padre occupa il livello superiore e l'elemento figlio occupa il livello inferiore.  
  
 La clausola che crea l'elemento figlio **Recordset** potrebbe ora essere un numero arbitrario di shape nidificati comandi COMPUTE, in cui il comando maggiormente annidato contiene la query con parametri. Il data shaping risultante **Recordset** dispone di più livelli, in cui l'elemento padre occupa il livello superiore, l'elemento figlio occupa il livello inferiore e un numero arbitrario di **Recordset**s generato dal comandi Shape calcolo occupano i livelli intermedi.  
  
 L'utilizzo tipico per questa funzionalità consiste nel richiamare la funzione di aggregazione e le funzionalità di raggruppamento di shapeCOMPUTE comandi per creare intermedi **Recordset** gli oggetti con le informazioni analitiche figlio **Recordset** . Inoltre, poiché si tratta di un comando di forma con parametri, ogni volta che una colonna a capitoli del padre si accede, un nuovo elemento figlio **Recordset** possono essere recuperati. Poiché i livelli intermedi sono derivati dall'elemento figlio, sono anche verrà ricalcolati.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)
