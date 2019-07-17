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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901437"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Aggiunta di un'origine dati Visual FoxPro
Per accedere a dati Visual FoxPro dall'applicazione, è necessario disporre di un'origine dati. È possibile creare un'origine dati come indicato di seguito:  
  
-   In un'applicazione, ad esempio Microsoft Word®, Microsoft Excel o Microsoft Access, che usa i driver ODBC.  
  
-   All'esterno dell'applicazione, tramite il Microsoft Windows® 95, Microsoft Windows 98 o pannello di controllo di Microsoft Windows/Windows 2000.  
  
 Dopo aver creato un'origine dati nel sistema, è possibile riusare la stessa origine dati ogni volta che si desidera accedere ai dati Visual FoxPro. Se si dispone di diversi database diversi o tabelle che si desidera accedere, è possibile creare un'origine dati separata per ogni database o una directory.  
  
 La procedura seguente crea un'origine dati utilizzando il pannello di controllo. Per altre informazioni su come creare un'origine dati da un'applicazione, vedere [l'accesso ai dati Visual FoxPro da Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Per aggiungere un'origine dati Visual FoxPro  
  
1.  Nei computer che eseguono Windows 2000, aprire il pannello di controllo di Windows e fare doppio clic su strumenti di amministrazione.  
  
2.  Fare doppio clic su origini dati (ODBC) per aprire la finestra di dialogo Amministrazione origine dati ODBC. Questa icona è disponibile dopo aver installato il Driver ODBC Visual FoxPro o qualsiasi software dei driver ODBC.  
  
    > [!NOTE]  
    >  Se si esegue una versione precedente di Windows, aprire il pannello di controllo di Windows e fare doppio clic su 32 bit ODBC o ODBC per aprire la finestra di dialogo Amministrazione origine dati ODBC.  
  
3.  Fare clic su Aggiungi.  
  
4.  Nella finestra di dialogo Crea nuova origine dati, selezionare Microsoft Visual FoxPro Driver e quindi fare clic su Fine.  
  
5.  Nel [finestra di dialogo di installazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), digitare il nome dell'origine dati e la descrizione, selezionare il tipo di database, selezionare il database o la directory e quindi fare clic su OK.  
  
     Il nuovo nome dell'origine dati viene visualizzato nell'elenco di origini dati utente nella scheda DSN utente della finestra di dialogo Amministrazione origine dati ODBC.  
  
6.  Fare clic su OK per salvare la nuova origine dati e chiudere la finestra di dialogo Amministrazione origine dati ODBC.
