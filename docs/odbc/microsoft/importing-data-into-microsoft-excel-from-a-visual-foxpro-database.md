---
title: Importazione di dati in Microsoft Excel da un Database di Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65635132c5f98b0565391122877f2e3c0a6714
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085551"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importazione di dati in Microsoft Excel da un database Visual FoxPro
Se è stata definita un'origine dati per tale, è possibile importare dati Visual FoxPro nel foglio di lavoro Microsoft Excel. Per informazioni sulla creazione di un'origine dati Visual FoxPro, vedere [l'accesso a un'origine dati Visual FoxPro da Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Per importare dati Visual FoxPro in un foglio di lavoro di Microsoft Excel  
  
1.  Aprire un foglio di calcolo di Microsoft Excel.  
  
2.  Dal menu di scelta dei dati, scegliere Recupera dati esterni. Verrà visualizzata la finestra di Query Microsoft.  
  
3.  Nella finestra di dialogo Seleziona origine dati, selezionare un'origine dati Visual FoxPro e quindi fare clic su utilizza.  
  
4.  Se il database a cui accede l'origine dati include tabelle, selezionare una tabella dalla finestra di dialogo Aggiungi tabelle. Query Microsoft consente di visualizzare la tabella aggiunta nella parte superiore della finestra di Progettazione query.  
  
    > [!NOTE]  
    >  L'elenco dei proprietari non è disponibile nella finestra di dialogo in quanto il driver non supporta i proprietari. Elenco dei Database non è disponibile perché il driver non supporta più database in un'origine dati.  
  
5.  Selezionare i campi per la query usando il trascinamento dalla tabella in basso metà della finestra di progettazione.  
  
6.  Chiudere Microsoft Query. I dati selezionati vengono importati nel foglio di calcolo Microsoft Excel.
