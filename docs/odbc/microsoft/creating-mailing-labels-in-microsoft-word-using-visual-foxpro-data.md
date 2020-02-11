---
title: Creazione di etichette di mailing in Microsoft Word mediante dati Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73880171493555a7d30e5c0c5419d02338961e9b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096517"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>Creazione di etichette indirizzo in Microsoft Word con i dati Visual FoxPro
È possibile usare dati Visual FoxPro in un documento di Microsoft Word per Windows 95 o Windows 98. Ad esempio, si potrebbe voler creare etichette di mailing dalle informazioni del cliente archiviate in una tabella di Visual FoxPro.  
  
### <a name="to-create-mailing-labels"></a>Per creare etichette di mailing  
  
1.  In Microsoft Word creare un nuovo documento vuoto.  
  
2.  Scegliere Stampa unione dal menu strumenti.  
  
3.  Nell'helper stampa unione scegliere Crea e quindi selezionare le etichette per la distribuzione.  
  
4.  In documento principale scegliere finestra attiva.  
  
5.  In origine dati scegliere Ottieni dati, quindi selezionare Apri origine dati.  
  
6.  Nella finestra di dialogo Apri origine dati scegliere MS query.  
  
7.  Nella finestra di dialogo Seleziona origine dati selezionare un'origine dati Visual FoxPro, quindi fare clic su USA.  
  
8.  Se il database a cui si accede dall'origine dati include tabelle, selezionare una tabella nella finestra di dialogo Aggiungi tabelle. Microsoft query consente di visualizzare la tabella aggiunta nella parte superiore della finestra Progettazione query.  
  
9. Selezionare i campi per la query trascinandoli dalla tabella sulla metà inferiore della finestra di progettazione.  
  
10. Scegliere Restituisci dati a Microsoft Word dal menu file. Microsoft query viene chiusa e i dati selezionati sono disponibili per l'utilizzo nel documento di merge della posta.  
  
11. In documento principale scegliere installazione.  
  
12. Nella finestra di dialogo Opzioni etichette selezionare la stampante e le informazioni sull'etichetta desiderata, quindi fare clic su OK.  
  
13. Nella finestra di dialogo Crea etichette selezionare i campi che si desidera stampare sulle etichette per il mailing, quindi fare clic su OK.  
  
14. Nell'helper stampa unione, in Unisci i dati con il documento, fare clic su Unisci.  
  
15. Nella finestra di dialogo Unisci selezionare le opzioni desiderate, quindi fare clic su Unisci.
