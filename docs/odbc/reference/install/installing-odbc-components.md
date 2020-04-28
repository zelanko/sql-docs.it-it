---
title: Installazione dei componenti ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298981"
---
# <a name="installing-odbc-components"></a>Installazione dei componenti ODBC
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 In questa sezione viene descritto il modo in cui vengono installati e rimossi i componenti ODBC. Poiché gli sviluppatori di driver installano sempre un componente ODBC (driver), devono leggere questa sezione. Gli sviluppatori di applicazioni devono leggere questa sezione solo se forniranno componenti ODBC con le applicazioni. I componenti ODBC includono Gestione driver, driver, convertitori, la DLL del programma di installazione, la libreria di cursori e tutti i file correlati. Ai fini di questa sezione, le applicazioni ODBC non vengono considerate componenti ODBC.  
  
> [!NOTE]  
>  Questa sezione è dedicata alle piattaforme Microsoft Windows. La modalità di installazione dei componenti ODBC in altre piattaforme è specifica della piattaforma.  
  
 I componenti ODBC vengono installati e rimossi in base ai singoli componenti, non a livello di file. Se, ad esempio, un traduttore è costituito dal traduttore stesso e da un numero di file di dati, questi file vengono installati e rimossi come gruppo. non devono essere installate e rimosse in base ai singoli file. Il motivo è quello di assicurarsi che nel sistema siano presenti solo i componenti completi.  
  
 Per l'installazione e la rimozione di componenti, vengono definiti i componenti ODBC seguenti:  
  
-   **Componenti di base.** Gestione driver, la libreria di cursori, la DLL del programma di installazione e qualsiasi altro file correlato costituiscono i componenti di base e devono essere installati e rimossi come gruppo.  
  
-   **Driver.** Ogni driver è un componente separato.  
  
-   **Traduttori.** Ogni traduttore è un componente separato.  
  
 Con il supporto di Unicode in ODBC 3,5 e versioni successive, è necessario considerare alcune considerazioni sull'utilizzo di OLE DB componenti con ODBC. La versione 1,1 del provider OLE DB per ODBC è stata scritta in specifiche Unicode specifiche all'interno di ODBC 3,0. Poiché queste specifiche sono state modificate in ODBC 3,5, è necessario disporre della versione 1,5 o successiva del provider quando si utilizza ODBC 3,5 e versioni successive. In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Componenti di installazione](../../../odbc/reference/install/installation-components.md)  
  
-   [Conteggio utilizzi](../../../odbc/reference/install/usage-counting.md)
