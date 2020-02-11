---
title: SQLParamOptions (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: 1adbde1b3df38d2b602f1ec42a2c96f36e8bd67b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996382"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 1  
  
 Consente a un'applicazione di specificare più valori per il set di parametri assegnati da [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). La possibilità di specificare più valori per un set di parametri è utile per gli inserimenti bulk e per altre operazioni che richiedono che l'origine dati elabori più volte la stessa istruzione SQL con diversi valori di parametro. Ad esempio, un'applicazione può specificare tre set di valori per il set di parametri associato a un'istruzione **Insert** , quindi eseguire l'istruzione **Insert** una volta per eseguire le tre operazioni di inserimento.  
  
 Per ulteriori informazioni, vedere [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) in *ODBC Programmer ' s Reference*.
