---
title: La connessione a un'origine dati (Driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adee8d8dd8d6db0d79b37ff853c41e7604fe21de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63302125"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Connessione a un'origine dati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Un'applicazione ODBC è possibile passare le informazioni di connessione in diversi modi. Ad esempio, l'applicazione potrebbe avere il driver Chiedi sempre conferma all'utente le informazioni di connessione. O l'applicazione potrebbe aspettarsi una stringa di connessione che specifica la connessione all'origine dati. Modalità di connessione a un'origine dati dipende dal metodo di connessione usato dall'applicazione ODBC.  
  
 Un modo comune per connettersi a un'origine dati è tramite la finestra di dialogo origine dati. Se l'applicazione ODBC è configurato per usare una finestra di dialogo, queste finestre di dialogo viene visualizzata e viene richiesto per le informazioni di connessione origine dati appropriata.  
  
 È anche possibile connettersi a un'origine dati usando il [stringa di connessione](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Per connettersi a un'origine dati tramite una finestra di dialogo  
  
1.  Quando viene visualizzata la finestra di dialogo origine dati, selezionare un'origine dati Oracle e quindi fare clic su OK. Viene visualizzata la finestra di dialogo Connetti.  
  
2.  Immettere le informazioni appropriate per la finestra di dialogo di connessione e quindi fare clic su OK.  
  
 Dopo la connessione informazioni vengono verificate, l'applicazione può usare il Driver ODBC per Oracle di accedere alle informazioni contenute nell'origine dati.
