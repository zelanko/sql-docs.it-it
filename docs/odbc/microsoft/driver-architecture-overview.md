---
title: Panoramica dell'architettura driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fdb1789c6640c072ec013c341bd4889b28bb469
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128086"
---
# <a name="driver-architecture-overview"></a>Panoramica dell'architettura del driver
Il Driver ODBC Microsoft Visual FoxPro è un driver a 32 bit che consente di aprire ed eseguire query su un database di Microsoft Visual FoxPro o FoxPro tabelle tramite l'interfaccia aprire Database Connectivity (ODBC). È possibile accedere ai dati di FoxPro utilizzando i tipi di applicazioni seguenti:  
  
-   Un'applicazione di Microsoft Office, ad esempio Microsoft Excel o Microsoft Word, che Usa Query di Microsoft per comunicare con ODBC.  
  
-   Un'applicazione scritta in Microsoft Visual C++ o C, che usa l'API SDK di ODBC.  
  
-   Un'applicazione scritta in Microsoft Visual Basic o Microsoft Visual Basic, Applications Edition.  
  
 In ogni caso, la richiesta di informazioni viene utilizzata l'API ODBC. Gestione Driver ODBC funziona con il Driver ODBC Visual FoxPro da aprire e recuperare dati dal database e tabelle FoxPro.  
  
 L'architettura è rappresentata nel diagramma seguente:  
  
 ![Architettura del Driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Terminologia di Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Installazione e configurazione del Driver ODBC Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Uso del driver ODBC Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
