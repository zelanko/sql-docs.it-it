---
description: MSSQLSERVER_9532
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4843631d2e387818b40520e0076cc22b32b10bc9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491116"
---
# <a name="mssqlserver_9532"></a>MSSQLSERVER_9532
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|9532|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Testo del messaggio|Conversione non riuscita del tipo di dati '%ls' nel tipo di dati '%ls' per la colonna '%.*ls' durante l'operazione query/DML che interessa il set di colonne '%.\*ls'.|  
  
## <a name="explanation"></a>Spiegazione  
Un set di colonne è una rappresentazione XML non tipizzata che combina alcune colonne di una tabella in un output strutturato. Quando i valori di una colonna di tipo sparse vengono inseriti o aggiornati utilizzando il set di colonne XML, i valori inseriti nelle colonne di tipo sparse sottostanti vengono convertiti implicitamente dal tipo di dati **xml**. Non è stato possibile convertire un valore specificato nel tipo di dati della colonna.  
  
## <a name="user-action"></a>Azione dell'utente  
Poiché il valore specificato non è stato convertito implicitamente, potrebbe costituire una voce non valida. Correggere l'errore e riprovare. Se il valore è corretto, modificare l'istruzione per utilizzare le colonne singole anziché il set di colonne. In questo modo sarà possibile eseguire esplicitamente il cast del valore nel tipo di dati corretto.  
  
