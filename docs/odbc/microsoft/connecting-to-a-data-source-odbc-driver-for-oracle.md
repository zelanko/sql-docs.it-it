---
description: Connessione a un'origine dati (driver ODBC per Oracle)
title: Connessione a un'origine dati (driver ODBC per Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6951dd89f3ad1a311d93aca460c61dc7317b2f30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483664"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Connessione a un'origine dati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Un'applicazione ODBC può passare le informazioni di connessione in diversi modi. Ad esempio, l'applicazione potrebbe chiedere al driver di richiedere sempre all'utente le informazioni di connessione. In alternativa, è possibile che l'applicazione preveda una stringa di connessione che specifichi la connessione all'origine dati. La modalità di connessione a un'origine dati dipende dal metodo di connessione utilizzato dall'applicazione ODBC.  
  
 Un modo comune per connettersi a un'origine dati è tramite la finestra di dialogo origine dati. Se l'applicazione ODBC è configurata per l'utilizzo di una finestra di dialogo, viene visualizzata la finestra di dialogo in cui vengono richieste le informazioni di connessione all'origine dati appropriate.  
  
 È inoltre possibile connettersi a un'origine dati utilizzando la [stringa di connessione](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Per connettersi a un'origine dati utilizzando una finestra di dialogo  
  
1.  Quando viene visualizzata la finestra di dialogo origine dati, selezionare un'origine dati Oracle e quindi fare clic su OK. Verrà visualizzata la finestra di dialogo Connetti.  
  
2.  Immettere le informazioni appropriate per la finestra di dialogo Connetti e quindi fare clic su OK.  
  
 Una volta verificate le informazioni di connessione, l'applicazione può utilizzare il driver ODBC per Oracle per accedere alle informazioni contenute nell'origine dati.
