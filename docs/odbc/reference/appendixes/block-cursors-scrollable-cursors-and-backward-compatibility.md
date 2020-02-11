---
title: Cursori a blocchi, cursori scorrevoli e compatibilità con le versioni precedenti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 433647481b2b73c22e00657c430d98177d3d4524
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125220"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti
L'esistenza di **SQLFetchScroll** e **SQLExtendedFetch** rappresenta la prima suddivisione chiara in ODBC tra l'API (Application Programming Interface), ovvero il set di funzioni chiamate dall'applicazione, e l'interfaccia del provider di servizi (SPI), ovvero il set di funzioni implementate dal driver. Questa suddivisione è necessaria in modo che ODBC *3. x*, che usa **SQLFetchScroll**, sia conforme agli standard e sia compatibile anche con ODBC *2. x*, che usa **SQLExtendedFetch**.  
  
 L'API ODBC *3. x* , ovvero il set di funzioni chiamate dall'applicazione, include **SQLFetchScroll** e gli attributi dell'istruzione correlati. ODBC *3. x* SPI, ovvero il set di funzioni implementate dal driver, include **SQLFetchScroll**, **SQLExtendedFetch**e gli attributi di istruzione correlati. Poiché ODBC non impone formalmente questa suddivisione tra l'API e il SPI, è possibile che le applicazioni ODBC *3. x* chiamino **SQLExtendedFetch** e gli attributi dell'istruzione correlati. A tale scopo, tuttavia, non esiste alcun motivo per l'applicazione ODBC *3. x* . Per ulteriori informazioni sulle API e SPIs, vedere Introduzione all' [architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni sulle funzioni e sugli attributi di istruzione che un'applicazione ODBC *3. x* deve utilizzare con i cursori Block e scroll, vedere [blocchi cursori, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3. x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Funzionamento di Gestione driver](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Funzionamento del driver](../../../odbc/reference/appendixes/what-the-driver-does.md)
