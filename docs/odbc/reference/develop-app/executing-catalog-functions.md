---
title: Funzioni di catalogo di esecuzione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6469a5394e232ab9d9135fbbbd56ba7b791ccbcb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305722"
---
# <a name="executing-catalog-functions"></a>Esecuzione delle funzioni di catalogo
Poiché una funzione di catalogo crea un set di risultati, equivale all'esecuzione di qualsiasi istruzione SQL che genera il set di risultati. Infatti, le funzioni di catalogo vengono spesso implementate eseguendo istruzioni SQL predefinite o chiamando procedure predefinite fornite con il driver o DBMS. Quasi tutto ciò che si applica alle istruzioni SQL che creano set di risultati si applica anche alle funzioni di catalogo. Ad esempio, l'attributo dell'istruzione SQL_ATTR_MAX_ROWS limita il numero di righe restituite dalla funzione di catalogo, così come limita il numero di righe restituite da un'istruzione **SELECT.**  
  
 Per eseguire una funzione di catalogo, un'applicazione chiama solo la funzione.  
  
 Per ulteriori informazioni sulle funzioni di catalogo, vedere [Funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).
