---
description: Indici dBASE
title: indici dBASE | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30a6390f0e187cc063b2a650af2da3b9fcc87d57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340957"
---
# <a name="dbase-indexes"></a>Indici dBASE
Il driver dBASE ODBC si apre e aggiorna automaticamente i file di indice di dBASE IV. È necessario utilizzare la finestra di dialogo **Seleziona indici** visualizzata tramite Amministrazione origine dati ODBC per associare i file di dBASE III. NDX con file dBASE.  
  
 Per la creazione di indici dBASE si applicano le limitazioni seguenti:  
  
-   Tutti i nomi di colonna devono essere validi.  
  
-   Tutte le colonne devono essere nello stesso ordine crescente o decrescente.  
  
-   La lunghezza di una singola colonna di testo deve essere inferiore a 100 byte.  
  
-   Se esiste più di una colonna, tutte le colonne devono essere colonne di testo e la somma delle dimensioni della colonna deve essere inferiore a 100 byte.  
  
-   I campi Memo non possono essere indicizzati.  
  
-   Non è necessario specificare un indice per il set di campi corrente, ovvero gli indici duplicati non sono consentiti.  
  
-   Il nome dell'indice deve corrispondere alla convenzione di denominazione degli indici dBASE. per dBASE III è necessario che ogni indice si trovi in un file separato, ognuno con estensione NDX. In dBASE IV gli indici vengono creati come nomi di Tag archiviati in un singolo file con estensione MDX. Il file con estensione MDX ha lo stesso nome di base del file di database (ad esempio, EMP. MDX è il file di indice per il database EMP. dbf).  
  
-   dBASE definisce un indice univoco in cui un solo record di un set con valori di chiave identici viene aggiunto all'indice.
