---
title: Liberazione di descrittori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe489222c026c1499135b716f0485bb04f51bad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069775"
---
# <a name="freeing-descriptors"></a>Rilascio di descrittori
Descrittori allocati in modo esplicito possono essere liberato uno in modo esplicito, chiamando **SQLFreeHandle** con *HandleType* di SQL_HANDLE_DESC o in modo implicito, viene liberata quando l'handle di connessione. Quando viene liberato un descrittore allocato in modo esplicito, tutti gli handle di istruzione a cui il descrittore liberato applicato automaticamente ripristinare i descrittori allocati in modo implicito per loro.  
  
 Descrittori allocati in modo implicito possono essere liberati solo chiamando **SQLDisconnect**, che elimina tutte le istruzioni o i descrittori di aprire la connessione, oppure chiamando **SQLFreeHandle** con un  *HandleType* SQL_HANDLE_STMT per liberare un handle di istruzione e tutti i descrittori allocati in modo implicito associati all'istruzione. Un descrittore allocato in modo implicito non possa essere liberato chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC.  
  
 Anche quando liberato, rimane valido, un descrittore allocato in modo implicito e **SQLGetDescField** può essere chiamata su relativi campi.
