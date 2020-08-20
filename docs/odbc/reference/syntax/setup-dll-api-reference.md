---
description: Informazioni di riferimento sull'API per l'installazione DLL
title: Informazioni di riferimento sull'API DLL di installazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cb3e20a1c25d206a1dd27367bbe4a128af0818f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487334"
---
# <a name="setup-dll-api-reference"></a>Informazioni di riferimento sull'API per l'installazione DLL
In questa sezione viene descritta la sintassi dell'API DLL di installazione driver, che è costituita da due funzioni (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** possono trovarsi nella dll del driver o in una DLL di installazione separata.  
  
 In questa sezione viene inoltre descritta la sintassi dell'API della DLL di installazione del convertitore, che è costituita da una singola funzione (**ConfigTranslator**). **ConfigTranslator** può essere presente nella DLL di conversione o in una DLL di installazione separata.  
  
 Ogni funzione è contrassegnata con la versione di ODBC in cui è stata introdotta.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Funzione ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Funzione ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Funzione ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
