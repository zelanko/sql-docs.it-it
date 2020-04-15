---
title: 'Passaggio 4b: Recuperare il conteggio delle righe Documenti Microsoft'
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
ms.openlocfilehash: 31ccbd15ae435165ea007fa9f3c0505c1dcc5aa0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302962"
---
# <a name="step-4b-fetch-the-row-count"></a>Passaggio 4b: Recuperare il conteggio delle righe
Il passaggio successivo consiste nel recuperare il conteggio delle righe, come illustrato nella figura seguente.  
  
 ![Recupero del conteggio delle righe](../../../odbc/reference/develop-app/media/pr15.gif "Pr15 (informazioni in stato di")  
  
 Se l'istruzione eseguita nel passaggio 3 è un'istruzione **UPDATE**, **DELETE**o **INSERT,** l'applicazione recupera il conteggio delle righe interessate con **SQLRowCount**. Per ulteriori informazioni, vedere [Determinazione del numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 L'applicazione torna ora al passaggio 3 per eseguire un'altra istruzione nella stessa transazione o procede al passaggio 5 per eseguire il commit o il rollback della transazione.
