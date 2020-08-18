---
description: Esecuzione delle funzioni di catalogo
title: Esecuzione di funzioni di catalogo | Microsoft Docs
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
ms.openlocfilehash: 19baae1518078c44b8e170fb623eab0087bac12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482914"
---
# <a name="executing-catalog-functions"></a>Esecuzione delle funzioni di catalogo
Poiché una funzione di catalogo crea un set di risultati, equivale all'esecuzione di qualsiasi istruzione SQL di generazione del set di risultati. Infatti, le funzioni di catalogo vengono spesso implementate eseguendo istruzioni SQL predefinite o chiamando procedure predefinite fornite con il driver o DBMS. Quasi tutto ciò che si applica alle istruzioni SQL per la creazione di set di risultati si applica anche alle funzioni di catalogo. L'attributo SQL_ATTR_MAX_ROWS Statement, ad esempio, limita il numero di righe restituite dalla funzione Catalog, così come limita il numero di righe restituite da un'istruzione **Select** .  
  
 Per eseguire una funzione di catalogo, un'applicazione chiama solo la funzione.  
  
 Per ulteriori informazioni sulle funzioni del catalogo, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).
