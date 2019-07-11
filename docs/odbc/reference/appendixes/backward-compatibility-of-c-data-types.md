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
manager: craigg
ms.openlocfilehash: eecc56b357b580d791d5c7c7b3fc7b57e99654fd
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794137"
---
# <a name="backward-compatibility-of-c-data-types"></a>Compatibilità con le versioni precedenti dei tipi di dati C
SQL_C_SHORT SQL_C_LONG e SQL_C_TINYINT sono stati sostituiti in ODBC da tipi signed che unsigned: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Un database ODBC *3.x* driver che dovrebbero lavorare con ODBC *2.x* le applicazioni devono supportare SQL_C_SHORT SQL_C_LONG e SQL_C_TINYINT, perché quando vengono chiamati, gestione Driver passa attraverso al autista.
