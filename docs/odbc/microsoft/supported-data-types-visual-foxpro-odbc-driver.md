---
title: Tipi di dati (Driver ODBC Visual FoxPro) supportati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cb48c5a763162685060a95e8d352ebddd8b0032
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270902"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipi di dati supportati (driver ODBC Visual FoxPro)
L'elenco di tipi di dati supportati dal driver vengono presentati tramite l'API ODBC e query di Microsoft.  
  
## <a name="data-types-in-c-applications"></a>Tipi di dati nelle applicazioni C  
 È possibile ottenere un elenco di tipi di dati supportati dal Driver ODBC Visual FoxPro con il [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) funzione nelle applicazioni C o C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipi di dati nelle applicazioni con Query di Microsoft  
 Se l'applicazione Usa Query di Microsoft per creare una nuova tabella in un'origine dati Visual FoxPro, Microsoft Query consente di visualizzare il **nuova definizione di tabella** nella finestra di dialogo. Sotto **descrizione del campo**, il **tipo** casella elenchi [tipi di dati Visual FoxPro campo](../../odbc/microsoft/visual-foxpro-field-data-types.md), rappresentato dai caratteri singoli.
