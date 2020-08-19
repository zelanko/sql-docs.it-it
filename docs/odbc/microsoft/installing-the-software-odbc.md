---
description: Installazione del software (ODBC)
title: Installazione del software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], installing
- installing ODBC driver for Oracle [ODBC]
ms.assetid: dfac8ade-eebe-4ebe-a199-feb740ed5bae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe161ef45ef91f67317d7a0b465e00d3d2045c40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449473"
---
# <a name="installing-the-software-odbc"></a>Installazione del software (ODBC)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver ODBC per Oracle è uno dei componenti di accesso ai dati. Accompagna altri componenti ODBC, ad esempio Amministrazione origine dati ODBC, e dovrebbe già essere installato. Il driver è disponibile anche in "driver e altri download" nel sito Web del servizio supporto tecnico Microsoft disponibile all'indirizzo [www.Microsoft.com](https://www.microsoft.com).  
  
 Il software di rete deve essere installato in base alla relativa documentazione. Il driver ODBC per Oracle non richiede particolari considerazioni sull'installazione purché il software di rete sia supportato.  
  
 È necessario installare il software Oracle in base alla relativa documentazione. Il driver ODBC per Oracle non richiede in genere considerazioni di installazione speciali, purché il driver supporti la versione. Tuttavia, per mantenere compatibili i prodotti, installare il driver ODBC per Oracle per verificare di disporre della versione più recente del driver. Oracle gestisce un sito FTP pubblico in cui inserisce, tra le altre cose, le patch per i prodotti server Oracle e il componente client fornito con i prodotti server. Queste patch sono necessarie per il corretto funzionamento di diversi prodotti e tecnologie Microsoft. Per ulteriori informazioni su questo sito, vedere [patch software Oracle](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!CAUTION]  
>  L'installazione di software Oracle su MDAC/Windows DAC può sovrascrivere le versioni correnti di MDAC. Se si verificano problemi utilizzando i componenti ODBC, reinstallare MDAC.
