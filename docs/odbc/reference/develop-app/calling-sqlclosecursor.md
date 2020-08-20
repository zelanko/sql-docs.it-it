---
description: Chiamata di SQLCloseCursor
title: Chiamata di SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 925617d79266f0b50ef9b38586b31af91311b63e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494771"
---
# <a name="calling-sqlclosecursor"></a>Chiamata di SQLCloseCursor
Poiché **SQLCloseCursor** è quasi uguale a **SQLFreeStmt** con SQL_CLOSE, gestione driver non esegue il mapping di questa funzione. Viene eseguito il mapping delle funzioni di sostituzione in modo che le applicazioni ODBC *2. x* esistenti possano passare facilmente a ODBC *3. x* usando le nuove funzioni. Questo tipo di spostamento rende più semplice per queste applicazioni iniziare a utilizzare la nuova funzionalità ODBC *3. x* all'interno del codice condizionale in modo modulare. **SQLCloseCursor** non rappresenta alcuna nuova funzionalità. Per un'applicazione non si ottengono vantaggi passando a **SQLCloseCursor** da **SQLFreeStmt** con SQL_CLOSE.
