---
title: "HelloData: Un'applicazione semplice ADO | Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 97957adf53cfea64693530b79920dd54d6d0a1bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700632"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: applicazione ADO semplice
I passaggi di questa semplice applicazione grazie a ognuna delle operazioni principali ADO: introduzione, l'analisi, la modifica e aggiornamento dei dati. Queste operazioni vengono eseguite sul database di esempio Northwind incluso in Microsoft® SQL Server. Per concentrare l'attenzione sui fondamenti di ADO e per evitare confusioni a livello di codice, gestione degli errori nell'esempio è minimo.  
  
### <a name="to-run-hellodata"></a>Per eseguire HelloData  
  
1.  Creare un nuovo progetto Standard EXE Visual Basic che fa riferimento alla libreria ADO. Per altre informazioni, vedere [riferimenti alle librerie ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Creare quattro pulsanti di comando nella parte superiore del form, impostando il **Name** e **didascalia** proprietà sui valori indicati nella tabella alla fine di questo argomento.  
  
3.  Sotto i pulsanti, aggiungere un **controllo DataGrid Microsoft** (Msdatgrd). Il file Msdatgrd è incluso in Visual Basic e si trova nella directory \windows\system32 o \Winnt\System32. Per aggiungere il controllo DataGrid al riquadro casella degli strumenti di Visual Basic, selezionare **componenti...**  dal **progetto** menu. Quindi selezionare la casella accanto a "controllo DataGrid Microsoft 6.0 (SP3) (OLEDB)" e quindi fare clic su **OK**. Per aggiungere il controllo al progetto, trascinare il controllo DataGrid dalla casella degli strumenti nel form di Visual Basic.  
  
4.  Creare un **casella di testo** nel form sotto la griglia e impostarne le proprietà come illustrato nella tabella. Il modulo dovrebbe essere simile nella figura seguente, al termine.  
  
5.  Infine, copiare il codice riportato nella [codice di HelloData](../../../ado/guide/data/hellodata-code.md)e incollarlo nella finestra dell'editor di codice del form. Premere **F5** per eseguire il codice.  
  
> [!NOTE]
>  Nell'esempio seguente e nel corso della Guida, l'id utente "Idpersonale" con una password di "123aBc" viene utilizzato per l'autenticazione con il server. È necessario sostituire questi valori con le credenziali di accesso valido per il server. Inoltre, sostituire il valore "MySQLServer" con il nome del server.  
  
 Per una descrizione dettagliata del codice, vedere [commenti su HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Mostra Form1 per l'applicazione VB HelloData](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo di controllo|Proprietà|Value|  
|------------------|--------------|-----------|  
|Form|Nome|Form1|  
||Altezza|6500|  
||Larghezza|6500|  
|DataGrid MS|Nome|grdDisplay1|  
|TextBox|Nome|txtDisplay1|  
||Proprietà Multiline|true|  
|Pulsante di comando|Nome|cmdGetData|  
||Didascalia|Get Data|  
|Pulsante di comando|Nome|cmdExamineData|  
||Didascalia|Esaminare i dati|  
|Pulsante di comando|nome|cmdEditData|  
||Didascalia|Modificare i dati|  
|Pulsante di comando|nome|cmdUpdateData|  
||Didascalia|Dati di aggiornamento|
