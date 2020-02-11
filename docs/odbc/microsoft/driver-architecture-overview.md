---
title: Panoramica dell'architettura del driver | Microsoft Docs
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
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071926"
---
# <a name="driver-architecture-overview"></a>Panoramica dell'architettura del driver
Il driver ODBC di Microsoft Visual FoxPro è un driver a 32 bit che consente di aprire ed eseguire query su un database di Microsoft Visual FoxPro o tabelle FoxPro tramite l'interfaccia Open Database Connectivity (ODBC). È possibile accedere ai dati di FoxPro usando i tipi di applicazioni seguenti:  
  
-   Applicazione Microsoft Office, ad esempio Microsoft Excel o Microsoft Word, che utilizza Microsoft query per comunicare con ODBC.  
  
-   Applicazione scritta in Microsoft Visual C++ o C che utilizza l'API ODBC SDK.  
  
-   Un'applicazione scritta in Microsoft Visual Basic o Microsoft Visual Basic, Applications Edition.  
  
 In ogni caso, la richiesta di informazioni utilizza l'API ODBC. Gestione driver ODBC funziona con il driver ODBC Visual FoxPro per aprire e recuperare i dati da tabelle e database di FoxPro.  
  
 L'architettura è rappresentata nel diagramma seguente:  
  
 ![Architettura del driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Terminologia di Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Installazione e configurazione del driver ODBC Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Uso del driver ODBC Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
