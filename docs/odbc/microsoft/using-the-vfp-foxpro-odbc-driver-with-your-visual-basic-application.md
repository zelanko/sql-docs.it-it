---
title: Usare il Driver ODBC VFP FoxPro con l'applicazione Visual Basic | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 017e8e7897b2b792d7a864dc336537d76dcad8b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087981"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Uso del driver ODBC VFP FoxPro con l'applicazione Visual Basic
Applicazione di Microsoft® Visual Basic® può comunicare con i dati Visual FoxPro mediante la creazione di un controllo dati che si connette a un'origine dati Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Per connettersi ai dati Visual FoxPro mediante il controllo dei dati in Visual Basic  
  
1.  Creare un'origine dati denominata "test" che si connette al database di esempio TasTrade incluso in Visual FoxPro. L'installazione di Visual FoxPro predefinita attiva del database di esempio TasTrade nel percorso:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  In Visual Basic, creare un nuovo modulo e inserire una casella di testo e un controllo dati su di esso.  
  
3.  Modifica proprietà di connessione del controllo dei dati come segue:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Modificare la proprietà RecordsetType come segue:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Modificare la proprietà di origine record come segue:  
  
    ```  
    customer  
    ```  
  
6.  Modificare la proprietà dell'origine dati per la casella di testo per il nome predefinito per il controllo dei dati al seguente:  
  
    ```  
    data1  
    ```  
  
7.  Modificare proprietà di DataField della casella di testo come segue:  
  
    ```  
    customer_id  
    ```  
  
8.  Eseguire il modulo e usare il controllo dei dati da ignorare attraverso i campi di id cliente dal database di esempio Visual FoxPro TasTrade.
