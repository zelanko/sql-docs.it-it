---
title: "Passaggio 1: Connettersi all'origine dati . Documenti Microsoft"
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a104733c0e5ec5acc87eeabd00c4e51d4bfd000
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301351"
---
# <a name="step-1-connect-to-the-data-source"></a>Passaggio 1: Connettersi all'origine dati
Il primo passaggio in qualsiasi applicazione consiste nel connettersi all'origine dati. Questa fase, incluse le funzioni necessarie, è illustrata nella figura seguente.  
  
 ![Connessione all'origine dati in un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11 (informazioni in due)")  
  
 Il primo passaggio per la connessione all'origine dati consiste nel caricare Gestione Driver e allocare l'handle di ambiente con **SQLAllocHandle**. Per ulteriori informazioni, vedere [Allocazione dell'handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 L'applicazione registra quindi la versione di ODBC a cui è conforme chiamando **SQLSetEnvAttr** con il SQL_ATTR_APP_ODBC_VERattributo di ambiente. Per ulteriori informazioni, vedere [Dichiarazione della versione ODBC dell'applicazione](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [Compatibilità con le versioni precedenti e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Successivamente, l'applicazione alloca un handle di connessione con **SQLAllocHandle** e si connette all'origine dati con **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**. Per ulteriori informazioni, vedere [Allocazione di un handle](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) di connessione e [creazione di una connessione](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 L'applicazione imposta quindi tutti gli attributi di connessione, ad esempio se eseguire manualmente il commit delle transazioni. Per ulteriori informazioni, vedere [Attributi di connessione](../../../odbc/reference/develop-app/connection-attributes.md).
