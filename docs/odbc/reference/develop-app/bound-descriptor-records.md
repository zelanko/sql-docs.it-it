---
title: 'Record del descrittore associato : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 155ef4951abddc7a73d9d4abfbc45248f33d653c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306308"
---
# <a name="bound-descriptor-records"></a>Record del descrittore associato
Quando l'applicazione imposta il campo SQL_DESC_DATA_PTR di un record del descrittore in modo che non contenga più un valore null, il record viene detto *associato*.  
  
 Se il descrittore è un APD, ogni record associato costituisce un parametro associato. Per i parametri di input, l'applicazione deve associare un parametro per ogni indicatore di parametro dinamico nell'istruzione SQL prima di eseguire l'istruzione. Per i parametri di output, l'applicazione non deve associare il parametro.  
  
 Se il descrittore è un ARD, che descrive una riga di dati del database, ogni record associato costituisce una colonna associata.
