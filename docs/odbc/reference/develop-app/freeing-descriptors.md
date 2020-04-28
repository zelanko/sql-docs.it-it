---
title: Liberare descrittori | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305602"
---
# <a name="freeing-descriptors"></a>Rilascio di descrittori
I descrittori allocati in modo esplicito possono essere liberati in modo esplicito, chiamando **SQLFreeHandle** con *HandleType* di SQL_HANDLE_DESC o in modo implicito quando viene liberato l'handle di connessione. Quando viene liberato un descrittore allocato in modo esplicito, tutti gli handle di istruzione a cui viene applicato il descrittore liberato vengono ripristinati automaticamente nei descrittori.  
  
 I descrittori allocati in modo implicito possono essere liberati solo tramite una chiamata a **Disconnect**, che elimina tutte le istruzioni o i descrittori aperti sulla connessione oppure chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT per liberare un handle di istruzione e tutti i descrittori allocati in modo implicito associati all'istruzione. Non è possibile liberare un descrittore allocato in modo implicito chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC.  
  
 Anche quando viene liberato, un descrittore allocato in modo implicito rimane valido e **SQLGetDescField** può essere chiamato sui campi.
