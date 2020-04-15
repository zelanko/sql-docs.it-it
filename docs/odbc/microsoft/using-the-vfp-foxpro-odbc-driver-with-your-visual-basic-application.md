---
title: Utilizzo del driver ODBC FoxPro VFP con l'applicazione Visual Basic . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292701"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Uso del driver ODBC VFP FoxPro con l'applicazione Visual Basic
L'applicazione Microsoft® Visual Basic® può comunicare con i dati di Visual FoxPro creando un controllo dati che si connette a un'origine dati Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Per connettersi ai dati di Visual FoxPro utilizzando il controllo dati in Visual Basic  
  
1.  Creare un'origine dati denominata "test" che si connette al database di esempio TasTrade incluso in Visual FoxPro.Create a data source named "test" that connects to the TasTrade sample database included in Visual FoxPro. L'installazione predefinita di Visual FoxPro inserisce il database di esempio TasTrade nel percorso:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  In Visual Basic creare un nuovo form e posizionarvi una casella di testo e un controllo Data.  
  
3.  Modificare la proprietà Connect del controllo Data come segue:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Modificare la proprietà RecordsetType nel modo seguente:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Modificare la proprietà RecordSource nel modo seguente:  
  
    ```  
    customer  
    ```  
  
6.  Modificare la proprietà DataSource per la casella di testo sul nome predefinito per il controllo Data nel modo seguente:  
  
    ```  
    data1  
    ```  
  
7.  Modificare la proprietà DataField della casella di testo nel modo seguente:  
  
    ```  
    customer_id  
    ```  
  
8.  Eseguire il modulo e utilizzare il controllo Dati per scorrere i campi dell'ID cliente dal database di esempio di Visual FoxPro TasTrade.
