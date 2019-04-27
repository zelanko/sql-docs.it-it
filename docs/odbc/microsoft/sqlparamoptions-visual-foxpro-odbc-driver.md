---
title: SQLParamOptions (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a66f0cd3a17baa9a09a5eeef2ade3d730f0a206b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636661"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 1  
  
 Consente a un'applicazione specificare più valori per il set di parametri assegnato dal [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). La possibilità di specificare più valori per un set di parametri è utile per gli inserimenti bulk e altre operazioni che richiedono l'origine dati per elaborare la stessa istruzione SQL più volte con diversi valori di parametro. Ad esempio, un'applicazione può specificare tre set di valori per il set di parametri associati un' **inserire** istruzione e quindi eseguire il **Inserisci** Inserisci istruzione una sola volta per eseguire le tre operazioni.  
  
 Per altre informazioni, vedere [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) nel *riferimento per programmatori ODBC*.
