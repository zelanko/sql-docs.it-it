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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65cc2ae8d2c2248a733e6efa9537fd3b40bb8fd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114116"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Passaggio 6: Disconnettersi dall'origine dati
Il passaggio finale consiste nel disconnettersi dall'origine dati, come illustrato nella figura seguente. In primo luogo, l'applicazione libera tutti gli handle di istruzione chiamando **SQLFreeHandle**. Per ulteriori informazioni, vedere la pagina relativa alla [liberazione di un handle di istruzione](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Disconnessione da un'origine dati](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Successivamente, l'applicazione si disconnette dall'origine dati con **SQLConnect** e libera l'handle di connessione con **SQLFreeHandle**. Per ulteriori informazioni, vedere [disconnessione da un'origine dati o da un driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Infine, l'applicazione libera l'handle di ambiente con **SQLFreeHandle** e Scarica Gestione driver. Per altre informazioni, vedere [allocazione dell'handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
