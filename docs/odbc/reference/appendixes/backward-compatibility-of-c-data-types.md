---
title: Compatibilità con le versioni precedenti dei tipi di dati C | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcfc4dd2ef1bee2783f073fbb85c0d911f84305a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037797"
---
# <a name="backward-compatibility-of-c-data-types"></a>Compatibilità con le versioni precedenti dei tipi di dati C
SQL_C_SHORT SQL_C_LONG e SQL_C_TINYINT sono stati sostituiti in ODBC da tipi signed che unsigned: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Un database ODBC *3.x* driver che dovrebbero lavorare con ODBC *2.x* le applicazioni devono supportare SQL_C_SHORT SQL_C_LONG e SQL_C_TINYINT, perché quando vengono chiamati, gestione Driver passa attraverso al autista.
