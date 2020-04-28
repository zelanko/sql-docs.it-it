---
title: "Passaggio 6: disconnettersi dall'origine dati | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df8cd94435d74bf813b0b64be0753a0beb44d354
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302792"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Passaggio 6: Disconnettersi dall'origine dati
Il passaggio finale consiste nel disconnettersi dall'origine dati, come illustrato nella figura seguente. In primo luogo, l'applicazione libera tutti gli handle di istruzione chiamando **SQLFreeHandle**. Per ulteriori informazioni, vedere la pagina relativa alla [liberazione di un handle di istruzione](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Disconnessione da un'origine dati](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Successivamente, l'applicazione si disconnette dall'origine dati con **SQLConnect** e libera l'handle di connessione con **SQLFreeHandle**. Per ulteriori informazioni, vedere [disconnessione da un'origine dati o da un driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Infine, l'applicazione libera l'handle di ambiente con **SQLFreeHandle** e Scarica Gestione driver. Per altre informazioni, vedere [allocazione dell'handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
