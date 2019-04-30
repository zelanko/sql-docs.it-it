---
title: Indici dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66dab60f4a9a180d2a8b74ce4d0c8f4d7bf8d242
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240400"
---
# <a name="dbase-indexes"></a>Indici dBASE
Il driver dBASE ODBC apre automaticamente e aggiorna i file degli indici dBASE IV. È necessario usare il **indici selezionare** finestra di dialogo visualizzata tramite Amministrazione origine dati ODBC per associare i file di dBASE III ndx ai file dBASE.  
  
 Per la creazione di indici dBASE si applicano le limitazioni seguenti:  
  
-   Tutti i nomi di colonna devono essere validi.  
  
-   Tutte le colonne devono essere in modo crescente o decrescente.  
  
-   La lunghezza di qualsiasi colonna di testo deve essere inferiore a 100 byte.  
  
-   Se è presente più di una colonna, tutte le colonne devono essere colonne di testo e la somma delle dimensioni di colonna deve essere inferiore a 100 byte.  
  
-   I campi di credito non possono essere indicizzati.  
  
-   Un indice non deve essere specificato per il set corrente di campi (vale a dire, gli indici duplicati non consentiti).  
  
-   Il nome dell'indice deve corrispondere la convenzione di denominazione indici dBASE. file dBASE III richiede che ogni indice sia in un file separato, ognuno dei quali con un'estensione ndx. In file dBASE IV, gli indici vengono creati come nomi di tag che sono archiviati in un file con estensione MDX singolo. Il file con estensione MDX ha lo stesso nome di base del file di database (ad esempio, emp è il file di indice per il database emp).  
  
-   file dBASE definisce un indice univoco come uno in cui viene aggiunto un solo record da un set con gli stessi valori chiave nell'indice.
