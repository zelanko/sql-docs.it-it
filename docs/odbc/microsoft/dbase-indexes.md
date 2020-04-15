---
title: Indici di dBASE Documenti Microsoft
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
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307672"
---
# <a name="dbase-indexes"></a>Indici dBASE
Il driver ODBC dBASE si apre e aggiorna i file di indice dBASE IV. È necessario utilizzare la finestra di dialogo **Seleziona indici** visualizzata tramite Amministrazione origine dati ODBC per associare i file dBASE III .ndx ai file dBASE.  
  
 Le limitazioni seguenti si applicano alla creazione di indici dBASE:  
  
-   Tutti i nomi di colonna devono essere validi.  
  
-   Tutte le colonne devono essere nello stesso ordine crescente o decrescente.  
  
-   La lunghezza di ogni singola colonna di testo deve essere inferiore a 100 byte.  
  
-   Se esiste più di una colonna, tutte le colonne devono essere colonne di testo e la somma delle dimensioni delle colonne deve essere inferiore a 100 byte.  
  
-   I campi Memo non possono essere indicizzati.  
  
-   Non è necessario specificare un indice per il set di campi corrente, ovvero gli indici duplicati non sono consentiti.  
  
-   Il nome dell'indice deve corrispondere alla convenzione di denominazione dell'indice dBASE. dBASE III richiede che ogni indice si svolda in un file separato, ciascuno con estensione .ndx. In dBASE IV, gli indici vengono creati come nomi di tag archiviati in un singolo file con estensione mdx. Il file con estensione mdx ha lo stesso nome di base del file di database (ad esempio, Emp.mdx è il file di indice per il database Emp.dbf).  
  
-   dBASE definisce un indice univoco come uno in cui all'indice viene aggiunto un solo record di un set con valori di chiave identici.
