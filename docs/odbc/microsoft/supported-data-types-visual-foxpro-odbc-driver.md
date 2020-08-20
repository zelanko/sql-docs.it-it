---
description: Tipi di dati supportati (driver ODBC Visual FoxPro)
title: Tipi di dati supportati (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04f2039d18f134fe2c48397f6c0dc987e97bf47d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471523"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipi di dati supportati (driver ODBC Visual FoxPro)
L'elenco dei tipi di dati supportati dal driver viene visualizzato tramite l'API ODBC e in Microsoft query.  
  
## <a name="data-types-in-c-applications"></a>Tipi di dati nelle applicazioni C  
 È possibile ottenere un elenco dei tipi di dati supportati dal driver ODBC Visual FoxPro utilizzando la funzione [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) nelle applicazioni C o C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipi di dati nelle applicazioni che usano Microsoft query  
 Se l'applicazione usa Microsoft query per creare una nuova tabella in un'origine dati Visual FoxPro, in Microsoft query viene visualizzata la finestra di dialogo **nuova definizione tabella** . In **Descrizione campo**, nella casella **tipo** sono elencati i [tipi di dati dei campi Visual FoxPro](../../odbc/microsoft/visual-foxpro-field-data-types.md), rappresentati da singoli caratteri.
