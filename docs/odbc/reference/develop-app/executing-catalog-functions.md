---
title: L'esecuzione di funzioni di catalogo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab6eba9c4a3df3e16e35d8a93dc95209a093fb80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901270"
---
# <a name="executing-catalog-functions"></a>Esecuzione delle funzioni di catalogo
Poiché una funzione di catalogo crea un set di risultati, è equivalente all'esecuzione di qualsiasi istruzione SQL che generano set di risultati. In effetti, funzioni di catalogo vengono spesso implementate l'esecuzione di istruzioni SQL predefinite o chiamando le procedure predefinite che vengono fornite con il driver o DBMS. Quasi tutto ciò che si applica alle istruzioni SQL che creano set di risultati si applica anche alle funzioni di catalogo. Ad esempio, l'attributo di istruzione SQL_ATTR_MAX_ROWS limita il numero di righe restituite dalla funzione di catalogo, esattamente come limita il numero di righe restituite da una **seleziona** istruzione.  
  
 Per eseguire una funzione di catalogo, un'applicazione chiama semplicemente la funzione.  
  
 Per altre informazioni sulle funzioni di catalogo, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).
