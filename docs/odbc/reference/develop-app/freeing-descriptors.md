---
title: Descrittori di Liberazione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305602"
---
# <a name="freeing-descriptors"></a>Rilascio di descrittori
I descrittori allocati in modo esplicito possono essere liberati in modo esplicito, chiamando **SQLFreeHandle** con *HandleType* di SQL_HANDLE_DESC, o in modo implicito, quando l'handle di connessione viene liberato. Quando un descrittore allocato in modo esplicito viene liberato, tutti gli handle di istruzione a cui è applicato il descrittore liberato ripristinano automaticamente i descrittori assegnati in modo implicito per essi.  
  
 I descrittori allocati in modo implicito possono essere liberati solo chiamando **SQLDisconnect**, che elimina tutte le istruzioni o i descrittori aperti sulla connessione, o chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT per liberare un handle di istruzione e tutti i descrittori allocati in modo implicito associati all'istruzione. Un descrittore allocato in modo implicito non può essere liberato chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC.  
  
 Anche quando viene liberato, un descrittore allocato in modo implicito rimane valido e **SQLGetDescField** può essere chiamato sui relativi campi.
