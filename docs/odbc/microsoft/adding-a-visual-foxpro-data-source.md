---
title: Aggiunta di un'origine dati di Visual FoxPro Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fd0c0f929ca00b7cf731dc92f07f69b6503f884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307142"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Aggiunta di un'origine dati Visual FoxPro
Per accedere ai dati di Visual FoxPro dall'applicazione, è necessario disporre di un'origine dati. È possibile creare un'origine dati come segue:You can create a data source as follows:  
  
-   In un'applicazione, ad esempio Microsoft® Word, Microsoft Excel o Microsoft Access, che utilizza driver ODBC.  
  
-   All'esterno dell'applicazione, utilizzare il Pannello di controllo di Microsoft Windows® 95, Microsoft Windows 98 o Microsoft Windows NT®/Windows 2000.  
  
 Dopo l'esecuzione di un'origine dati nel sistema, è possibile riutilizzare la stessa origine dati ogni volta che si desidera accedere ai dati di Visual FoxPro. Se si desidera accedere a diversi database o tabelle a cui si desidera accedere, è possibile creare un'origine dati separata per ogni database o directory.  
  
 La procedura seguente crea un'origine dati utilizzando il Pannello di controllo. Per ulteriori informazioni su come creare un'origine dati da un'applicazione, vedere [Accesso ai dati di Visual FoxPro da Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Per aggiungere un'origine dati Visual FoxPro  
  
1.  Nei computer che eseguono Windows 2000, aprire il Pannello di controllo di Windows e fare doppio clic su Strumenti di amministrazione.  
  
2.  Fare doppio clic su Origini dati (ODBC) per aprire la finestra di dialogo Amministratore origine dati ODBC. Questa icona è disponibile dopo aver installato il driver ODBC di Visual FoxPro o qualsiasi software del driver ODBC.  
  
    > [!NOTE]  
    >  Se si esegue una versione precedente di Windows, aprire il Pannello di controllo di Windows e fare doppio clic su ODBC o ODBC a 32 bit per aprire la finestra di dialogo Amministratore origine dati ODBC.  
  
3.  Fare clic su Aggiungi.  
  
4.  Nella finestra di dialogo Crea nuova origine dati selezionare Driver Microsoft Visual FoxPro e quindi fare clic su Fine.  
  
5.  Nella finestra di [dialogo Installazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)digitare il nome e la descrizione dell'origine dati, selezionare il tipo di database, selezionare il database o la directory e quindi fare clic su OK.  
  
     Il nome della nuova origine dati viene visualizzato nell'elenco Origini dati utente nella scheda DSN utente della finestra di dialogo Amministratore origine dati ODBC.  
  
6.  Fare clic su OK per salvare la nuova origine dati e chiudere la finestra di dialogo Amministratore origine dati ODBC.
