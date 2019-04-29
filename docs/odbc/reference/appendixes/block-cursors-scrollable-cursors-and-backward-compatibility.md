---
title: Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d3896473a1fa08f769f13d94bd1d81f373cf67c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026603"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti
La presenza di entrambe **SQLFetchScroll** e **SQLExtendedFetch** rappresenta cancellare le prima di tutto è suddiviso in ODBC tra l'interfaccia API (Application Programming), ovvero il set di funzioni di le chiamate dell'applicazione e il servizio Provider di interfaccia (SPI), ovvero il set di funzioni il driver implementa. Questa suddivisione è necessaria in modo che ODBC 3. *x*, che usa **SQLFetchScroll**, bealigned con gli standard e anche essere compatibile con ODBC 2. *x*, che usa **SQLExtendedFetch**.  
  
 ODBC 3 *. x* API, ovvero il set di funzioni l'applicazione chiama, includono **SQLFetchScroll** e relativi attributi di istruzione. ODBC 3 *. x* SPI, ovvero il set di funzioni implementa il driver, include **SQLFetchScroll**, **SQLExtendedFetch**e i relativi attributi di istruzione. Poiché ODBC non impone formalmente questa suddivisione tra l'API e di SPI, è possibile che per ODBC 3 *. x* alle applicazioni di chiamare **SQLExtendedFetch** e relativi attributi di istruzione. Tuttavia, non vi è alcun motivo per ODBC 3*x* dell'applicazione per eseguire questa operazione. Per altre informazioni sulle API e SPI, vedere l'introduzione [architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni su quali funzioni e l'istruzione di attributi un'applicazione ODBC 3. *x* dell'applicazione deve usare con i cursori scorrevoli e blocco, vedere [cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Come funziona Gestione driver](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Come funziona il driver](../../../odbc/reference/appendixes/what-the-driver-does.md)
