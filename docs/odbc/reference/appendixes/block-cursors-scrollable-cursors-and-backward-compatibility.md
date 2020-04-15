---
title: Cursori a blocchi, cursori scorrevoli e compatibilità con le versioni precedenti. Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe24362f1a49577a7fb494f768947080d0ab6e9e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292311"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti
L'esistenza di **SQLFetchScroll** e **SQLExtendedFetch** rappresenta la prima netta divisione in ODBC tra l'API (Application Programming Interface), ovvero l'insieme di funzioni chiamate dall'applicazione, e l'interfaccia del provider di servizi (SPI), ovvero l'insieme di funzioni implementate dal driver. Questa divisione è necessaria in modo che ODBC *3.x*, che utilizza **SQLFetchScroll**, sia allineato agli standard ed essere compatibile con ODBC *2.x*, che utilizza **SQLExtendedFetch**.  
  
 L'API ODBC *3.x,* ovvero il set di funzioni chiamate dall'applicazione, include **SQLFetchScroll** e gli attributi dell'istruzione correlata. ODBC *3.x* SPI, che è l'insieme di funzioni implementato dal driver, include **SQLFetchScroll**, **SQLExtendedFetch**e gli attributi dell'istruzione correlata. Poiché ODBC non applica formalmente questa divisione tra l'API e spi, è possibile che le applicazioni ODBC *3.x* chiamino **SQLExtendedFetch** e gli attributi di istruzione correlati. Tuttavia, non vi è alcun motivo per l'applicazione ODBC *3.x* per eseguire questa operazione. Per ulteriori informazioni su API e IPO, vedere l'introduzione [all'architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni sulle funzioni e gli attributi dell'istruzione che un'applicazione ODBC *3.x* deve utilizzare con i cursori a blocchi e scorrevoli, vedere Cursori a [blocchi, cursori scorrevoli e Compatibilità con](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)le versioni precedenti per le applicazioni ODBC 3.x .  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Come funziona Gestione driver](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Come funziona il driver](../../../odbc/reference/appendixes/what-the-driver-does.md)
