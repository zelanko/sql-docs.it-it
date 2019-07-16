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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf2ef856d8970bf60b3f1f329c57a2379eb528dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094017"
---
# <a name="installing-odbc-components"></a>Installazione dei componenti ODBC
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Questa sezione descrive come i componenti ODBC vengono installati e rimossi. Poiché gli sviluppatori di driver installare sempre un componente ODBC (i driver), devono leggere questa sezione. Gli sviluppatori di applicazioni necessario leggere questa sezione solo se sono verranno inclusi i componenti ODBC con le proprie applicazioni. Componenti ODBC includono gestione Driver, driver, funzioni di conversione, il programma di installazione DLL, la libreria di cursori e tutti i file correlati. Ai fini di questa sezione, le applicazioni ODBC non sono considerate componenti ODBC.  
  
> [!NOTE]  
>  In questa sezione è specifica per le piattaforme Microsoft Windows. Modalità di installazione dei componenti ODBC in altre piattaforme è specifica della piattaforma.  
  
 Componenti ODBC vengono installati e rimossi in modo da singoli componenti, non una base file per file. Ad esempio, se una funzione di conversione è costituita da del convertitore stesso e un numero di file di dati, questi file sono installati e rimossi come un gruppo. non devono essere installati e rimossi in una base file per file. Il motivo è assicurarsi che completi solo componenti presenti nel sistema.  
  
 Ai fini di installazione e rimozione di componenti, di seguito viene definiti i componenti ODBC:  
  
-   **Componenti di base.** Gestione Driver, libreria di cursori, programma di installazione di DLL e qualsiasi altro correlati file costituiscono i componenti di base e devono essere installati e rimosso come gruppo.  
  
-   **Driver.** Ogni driver è un componente separato.  
  
-   **Funzioni di conversione.** Ogni Microsoft translator è un componente separato.  
  
 Con il supporto di Unicode in ODBC 3.5 e versioni successive, alcune considerazione deve essere concessa a usando componenti OLE DB a ODBC. La versione 1.1 del Provider OLE DB per ODBC è stata scritta in base alle specifiche Unicode specifici all'interno di ODBC 3.0. Poiché queste specifiche modificato in ODBC 3.5, è necessario disporre di versione 1.5 o versioni successive del provider quando si utilizza ODBC 3.5 e versioni successive. In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Componenti di installazione](../../../odbc/reference/install/installation-components.md)  
  
-   [Conteggio utilizzi](../../../odbc/reference/install/usage-counting.md)
