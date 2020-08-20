---
description: Uso dei sinonimi con le stored procedure
title: Utilizzo di sinonimi con stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c0f210aad903dec6b29df2ca1bd121b569c4335
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471303"
---
# <a name="using-synonyms-with-stored-procedures"></a>Uso dei sinonimi con le stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Microsoft ODBC driver for Oracle Versions 2,0 e 2,5 non supporta i sinonimi durante la chiamata di stored procedure Oracle. I sinonimi funzionano come previsto quando vengono usati con altri oggetti di database Oracle, ad esempio le tabelle.
