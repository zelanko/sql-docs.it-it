---
title: Compatibilità con le versioni precedenti dei tipi di dati C Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a89b282a2229b6f34833b4371081661ea51b231
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304586"
---
# <a name="backward-compatibility-of-c-data-types"></a>Compatibilità con le versioni precedenti dei tipi di dati C
SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT sono stati sostituiti in ODBC da tipi con segno e senza segno: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Un driver ODBC *3.x* che deve funzionare con le applicazioni ODBC *2.x* deve supportare SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, perché quando vengono chiamati, Gestione Driver li passa al driver.
