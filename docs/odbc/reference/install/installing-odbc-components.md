---
title: Installazione dei componenti ODBC - Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298981"
---
# <a name="installing-odbc-components"></a>Installazione dei componenti ODBC
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare ODBC in modo esplicito solo nelle versioni precedenti di Windows.  
  
 In questa sezione viene descritta la modalità di installazione e rimozione dei componenti ODBC. Poiché gli sviluppatori di driver installano sempre un componente ODBC (il driver), è necessario leggere questa sezione. Gli sviluppatori di applicazioni devono leggere questa sezione solo se verranno fornite componenti ODBC con le applicazioni. I componenti ODBC includono Gestione Driver, driver, traduttori, la DLL del programma di installazione, la libreria di cursori e tutti i file correlati. Ai fini di questa sezione, le applicazioni ODBC non sono considerate componenti ODBC.  
  
> [!NOTE]  
>  Questa sezione è specifica per le piattaforme Microsoft Windows.This section is specific to Microsoft Windows platforms. La modalità di installazione dei componenti ODBC in altre piattaforme è specifica della piattaforma.  
  
 I componenti ODBC vengono installati e rimossi in base al componente, non file per file. Ad esempio, se un traduttore è costituito dal traduttore stesso e da un certo numero di file di dati, questi file vengono installati e rimossi come gruppo; non devono essere installati e rimossi file per file. Il motivo è assicurarsi che nel sistema siano presenti solo componenti completi.  
  
 Ai fini dell'installazione e della rimozione di componenti, i seguenti elementi sono definiti come componenti ODBC:  
  
-   **Componenti di base.** Gestione Driver, libreria di cursori, DLL del programma di installazione e qualsiasi altro file correlato costituiscono i componenti principali e devono essere installati e rimossi come gruppo.  
  
-   **Driver.** Ogni driver è un componente separato.  
  
-   **Traduttori.** Ogni traduttore è un componente separato.  
  
 Con il supporto di Unicode in ODBC 3.5 e versioni successive, è necessario prendere in considerazione l'utilizzo di componenti OLE DB con ODBC. The 1.1 version of the OLE DB Provider for ODBC was written to specific Unicode specifications within ODBC 3.0. Poiché queste specifiche sono state modificate in ODBC 3.5, è necessario disporre della versione 1.5 o successiva del provider quando si utilizza ODBC 3.5 e versioni successive. In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Componenti di installazione](../../../odbc/reference/install/installation-components.md)  
  
-   [Conteggio utilizzi](../../../odbc/reference/install/usage-counting.md)
