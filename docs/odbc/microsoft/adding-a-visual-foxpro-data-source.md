---
title: Aggiunta di un'origine dati Visual FoxPro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5203a7216faa008aade21c4e3e1dc54fc794461b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901437"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Aggiunta di un'origine dati Visual FoxPro
Per accedere ai dati Visual FoxPro dall'applicazione, è necessario disporre di un'origine dati. È possibile creare un'origine dati come segue:  
  
-   In un'applicazione, ad esempio Microsoft® Word, Microsoft Excel o Microsoft Access, che utilizza i driver ODBC.  
  
-   All'esterno dell'applicazione, utilizzando il pannello di controllo Microsoft Windows® 95, Microsoft Windows 98 o Microsoft Windows NT®/Windows 2000.  
  
 Dopo che un'origine dati è presente nel sistema, è possibile riutilizzare la stessa origine dati ogni volta che si desidera accedere ai dati Visual FoxPro. Se si dispone di più database o tabelle a cui si desidera accedere, è possibile creare un'origine dati distinta per ogni database o directory.  
  
 La procedura seguente consente di creare un'origine dati tramite il pannello di controllo. Per ulteriori informazioni su come creare un'origine dati da un'applicazione, vedere [accesso ai dati Visual FoxPro da Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Per aggiungere un'origine dati Visual FoxPro  
  
1.  Nei computer che eseguono Windows 2000, aprire il pannello di controllo di Windows e fare doppio clic su strumenti di amministrazione.  
  
2.  Fare doppio clic su origini dati (ODBC) per aprire la finestra di dialogo Amministrazione origine dati ODBC. Questa icona è disponibile dopo aver installato il driver ODBC Visual FoxPro o qualsiasi software per driver ODBC.  
  
    > [!NOTE]  
    >  Se si esegue una versione precedente di Windows, aprire il pannello di controllo di Windows e fare doppio clic su ODBC o ODBC a 32 bit per aprire la finestra di dialogo Amministrazione origine dati ODBC.  
  
3.  Fare clic su Aggiungi.  
  
4.  Nella finestra di dialogo Crea nuova origine dati selezionare Microsoft Visual FoxPro driver, quindi fare clic su fine.  
  
5.  Nella finestra di [dialogo Configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)Digitare il nome e la descrizione dell'origine dati, selezionare il tipo di database, selezionare il database o la directory, quindi fare clic su OK.  
  
     Il nuovo nome dell'origine dati viene visualizzato nell'elenco origini dati utente nella scheda DSN utente della finestra di dialogo Amministrazione origine dati ODBC.  
  
6.  Fare clic su OK per salvare la nuova origine dati e chiudere la finestra di dialogo Amministrazione origine dati ODBC.
