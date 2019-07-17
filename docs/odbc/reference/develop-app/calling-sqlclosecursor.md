---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 447a0892049317813fa9fe6986e6219922a11e28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068695"
---
# <a name="calling-sqlclosecursor"></a>Chiamata di SQLCloseCursor
In quanto **SQLCloseCursor** è quasi identico **SQLFreeStmt** con SQL_CLOSE, gestione Driver non esegue il mapping a questa funzione. Funzioni di sostituzione vengono mappate in modo che esistente ODBC *2.x* spostare facilmente le applicazioni a ODBC *3.x* usando le nuove funzioni. Tale cambiamento rende più semplice per tali applicazioni iniziare a usare nuovi ODBC *3.x* funzionalità all'interno di codice condizionale in modo modulare. **SQLCloseCursor** non rappresenta alcuna nuova funzionalità. Un'applicazione non riuscirà a ottenere alcun vantaggio spostando **SQLCloseCursor** dalla **SQLFreeStmt** con SQL_CLOSE.
