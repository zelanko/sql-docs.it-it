---
description: Comandi con parametri con comandi COMPUTE intermedi
title: Comandi con parametri con comandi di calcolo intermedi | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f5e4edf28f14763d4a7592f018f47135cae9981
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453093"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Comandi con parametri con comandi COMPUTE intermedi
Un comando APPEND Shape con parametri tipico include una clausola che crea un **Recordset** padre con un comando di query e un'altra clausola che crea un **Recordset** figlio con un comando di query con parametri, ovvero un comando contenente un segnaposto di parametro (un punto interrogativo, "?"). Il **Recordset** con forma risultante ha due livelli, in cui l'elemento padre occupa il livello superiore e l'elemento figlio occupa il livello inferiore.  
  
 La clausola che crea il **Recordset** figlio può ora essere un numero arbitrario di comandi di calcolo con forme annidate, in cui il comando più profondamente annidato contiene la query con parametri. Il **Recordset** a forma di risultante ha più livelli, in cui l'elemento padre occupa il livello superiore, l'elemento figlio occupa il livello selezionato e un numero arbitrario di **Recordset**generati dai comandi di calcolo della forma occupano i livelli interessati.  
  
 L'utilizzo tipico di questa funzionalità consiste nel richiamare la funzione di aggregazione e le capacità di raggruppamento dei comandi shapeCOMPUTE per creare oggetti **Recordset** che interessano le informazioni analitiche sul **Recordset**figlio. Inoltre, poiché si tratta di un comando Shape con parametri, ogni volta che si accede a una colonna del capitolo dell'elemento padre, è possibile recuperare un nuovo **Recordset** figlio. Poiché i livelli di intervento sono derivati dall'elemento figlio, verranno ricalcolati.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)
