---
title: "Passaggio 1: Connettersi all'origine dei dati | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80f2dfc05d9d27f60aca414ee0abd13e13b3ea65
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114266"
---
# <a name="step-1-connect-to-the-data-source"></a>Passaggio 1: Connettersi all'origine dati
Il primo passaggio in qualsiasi applicazione consiste nella connessione all'origine dati. Questa fase, incluse le funzioni che richiede, è illustrata nella figura seguente.  
  
 ![Connessione all'origine dei dati in un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 Il primo passaggio per la connessione all'origine dati viene caricato in Gestione Driver e allocare l'handle di ambiente con **SQLAllocHandle**. Per altre informazioni, vedere [allocare l'Handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Quindi, l'applicazione registra la versione di ODBC in cui è conforme chiamando **SQLSetEnvAttr** con l'attributo di ambiente SQL_ATTR_APP_ODBC_VER. Per altre informazioni, vedere [dichiarazione della versione dell'applicazione ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [garantire la compatibilità e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Successivamente, l'applicazione viene allocato un handle di connessione con **SQLAllocHandle** e si connette all'origine dati con **SQLConnect**, **SQLDriverConnect**, oppure **SQLBrowseConnect**. Per altre informazioni, vedere [allocare un Handle di connessione](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) e [stabilire una connessione](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 Quindi, l'applicazione imposta gli attributi di connessione, ad esempio se si desidera eseguire manualmente il commit delle transazioni. Per altre informazioni, vedere [attributi di connessione](../../../odbc/reference/develop-app/connection-attributes.md).
