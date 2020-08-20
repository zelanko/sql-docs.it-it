---
description: Uso del driver ODBC VFP FoxPro con l'applicazione Visual Basic
title: Usare il driver ODBC di VFP FoxPro con l'applicazione Visual Basic | Microsoft Docs
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
ms.openlocfilehash: 07ec83ccab43890bccbf5e12582628fdb98d29c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500054"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Uso del driver ODBC VFP FoxPro con l'applicazione Visual Basic
L'applicazione Microsoft® Visual Basic® può comunicare con dati Visual FoxPro creando un controllo dati che si connette a un'origine dati Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Per connettersi ai dati Visual FoxPro usando il controllo dati in Visual Basic  
  
1.  Creare un'origine dati denominata "test" che si connette al database di esempio TasTrade incluso in Visual FoxPro. L'installazione predefinita di Visual FoxPro posiziona il database di esempio TasTrade nel percorso:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  In Visual Basic creare un nuovo form e inserire una casella di testo e un controllo dati.  
  
3.  Modificare la proprietà Connect del controllo dati come segue:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Modificare la proprietà RecordsetType nel modo seguente:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Modificare la proprietà requests come segue:  
  
    ```  
    customer  
    ```  
  
6.  Modificare la proprietà DataSource della casella di testo con il nome predefinito per il controllo dati come segue:  
  
    ```  
    data1  
    ```  
  
7.  Modificare la proprietà DataField della casella di testo nel modo seguente:  
  
    ```  
    customer_id  
    ```  
  
8.  Eseguire il modulo e usare il controllo dati per ignorare i campi ID cliente dal database di esempio TasTrade di Visual FoxPro.
