---
description: 'Passaggio 4b: Recuperare il conteggio delle righe'
title: 'Passaggio 4b: recuperare il numero di righe | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eab5e1e1bf7eba70e2d84b36349e2f982a0b14c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494604"
---
# <a name="step-4b-fetch-the-row-count"></a>Passaggio 4b: Recuperare il conteggio delle righe
Il passaggio successivo consiste nel recuperare il conteggio delle righe, come illustrato nella figura seguente.  
  
 ![Recupero del conteggio delle righe](../../../odbc/reference/develop-app/media/pr15.gif "PR15")  
  
 Se l'istruzione eseguita nel passaggio 3 è un'istruzione **Update**, **Delete**o **Insert** , l'applicazione recupera il numero di righe interessate con **SQLRowCount**. Per ulteriori informazioni, vedere [determinazione del numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 L'applicazione ora torna al passaggio 3 per eseguire un'altra istruzione nella stessa transazione o procede al passaggio 5 per eseguire il commit o il rollback della transazione.
