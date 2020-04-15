---
title: Cenni preliminari sull'architettura dei driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd55290e09fbd35f5a1559ce4209693ef8eaaf73
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303462"
---
# <a name="driver-architecture-overview"></a>Panoramica dell'architettura del driver
Il driver ODBC di Microsoft Visual FoxPro è un driver a 32 bit che consente di aprire ed eseguire query su un database Microsoft Visual FoxPro o tabelle FoxPro tramite l'interfaccia ODBC (Open Database Connectivity). È possibile accedere ai dati FoxPro utilizzando i seguenti tipi di applicazioni:  
  
-   Un'applicazione di Microsoft Office, ad esempio Microsoft Excel o Microsoft Word, che utilizza Microsoft Query per comunicare con ODBC.  
  
-   Un'applicazione scritta in Microsoft Visual C , C o C che utilizza l'API ODBC SDK.  
  
-   Un'applicazione scritta in Microsoft Visual Basic o Microsoft Visual Basic, Applications Edition.  
  
 In ogni caso, la richiesta di informazioni utilizza l'API ODBC. Gestione ODBC Driver funziona con il driver ODBC di Visual FoxPro per aprire e recuperare dati da tabelle e database FoxPro.  
  
 L'architettura è rappresentata nel diagramma seguente:The architecture is represented in the following diagram:  
  
 ![Architettura del driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch (vfparch)")  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Terminologia di Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Installazione e configurazione del driver ODBC di Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Uso del driver ODBC Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
