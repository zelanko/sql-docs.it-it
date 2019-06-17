---
title: Patch del Software Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a4ac67e1a593cdfd7e67d789289bd1a5ece1467
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63233577"
---
# <a name="oracle-software-patches"></a>Patch del software Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Patch per i prodotti server Oracle e il relativo componente client sono necessarie per il funzionamento corretto di diversi prodotti e tecnologie Microsoft, tra cui il Driver ODBC di Microsoft per Oracle, il Provider Microsoft OLE DB per Oracle, informazioni su Internet Services (IIS), Servizi componenti (o Microsoft Transaction Server, se si utilizza Windows NT), e così via.  
  
> [!NOTE]  
>  Le istruzioni seguenti potrebbero non essere perfettamente accurate perché il sito FTP Oracle è soggette a modifiche.  
  
### <a name="to-download-the-oracle-software-patches"></a>Per scaricare le patch di software Oracle  
  
1.  Connettersi al sito FTP pubblico ftp.oracle.com di oracle. L'ID utente è "anonymous" e la password è il tuo indirizzo di posta elettronica.  
  
2.  Passare alla directory seguente: /server/wgt_tech/server/windowsNT.  
  
3.  Per scaricare le patch più rilevanti per Windows 95, Windows 98 e Windows NT o Windows 2000, spostarsi nella sottodirectory per la versione di Oracle - 7.3 o 8.0. Le due sottodirectory sono /73patchsets e /80patchsets.  
  
4.  Per scaricare le patch per la tecnologia di rete di Oracle, SQL * Net o Net8, passare alla directory seguente: / di rete.  
  
 Accedere al sito FTP dal Web browser potrebbe non funzionare. Se si verificano problemi, provare a usare un client FTP "tradizionale" oppure usare il prompt dei comandi DOS.  
  
> [!NOTE]  
>  Perché Oracle consente di correggere i bug nelle versioni correnti e quindi li retrofits alle versioni precedenti con patch software, è consigliabile scaricare la patch più recente disponibile. Ciò vale soprattutto per i componenti Client di Server Oracle. Se hai domande sull'installazione di patch, contattare il supporto di Oracle.
