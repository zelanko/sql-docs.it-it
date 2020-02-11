---
title: Importazione di dati Visual FoxPro in Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 557b5505b9eb6a15080a7d0495df2e63aefd2d76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085539"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importazione di dati Visual FoxPro in Microsoft Access
È possibile importare i dati archiviati in un database Visual FoxPro in un database di Microsoft Access usando l'opzione di importazione.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Per importare dati Visual FoxPro in un database di Microsoft Access  
  
1.  Aprire un database di Microsoft Access.  
  
2.  Scegliere Ottieni dati esterni dal menu file e quindi importa.  
  
3.  Nella finestra di dialogo Importa selezionare database ODBC nell'elenco tipo file.  
  
4.  Nella finestra di dialogo origini dati SQL selezionare l'origine dati Visual FoxPro che si connette ai dati FoxPro su cui si vuole eseguire la query e fare clic su OK.  
  
5.  Nella finestra di dialogo Importa oggetti selezionare una o più tabelle che si desidera importare, quindi fare clic su OK. I nomi delle tabelle di Visual FoxPro importati vengono visualizzati nella scheda tabelle del database di Microsoft Access.  
  
 È ora possibile usare Microsoft Access per modificare i dati nelle tabelle di Visual FoxPro importate. I dati importati sono uno snapshot dei dati archiviati in Visual FoxPro. le modifiche apportate ai dati importati non vengono restituite all'origine dati Visual FoxPro.  
  
 Per modificare i dati nell'origine dati Visual FoxPro, vedere [esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
