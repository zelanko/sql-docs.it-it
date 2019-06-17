---
title: Informazioni su driver e origini dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69516a613cbd9071686067350ced2ce5ca166a27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294447"
---
# <a name="about-drivers-and-data-sources"></a>Informazioni su driver e origini dati
*I driver* sono elencati i componenti che elaborano le richieste ODBC e restituiscono dati all'applicazione. Se necessario, i driver di modificare la richiesta di un'applicazione in un formato riconosciuto dall'origine dati. Per aggiungere o eliminare un driver dal computer, è necessario utilizzare il programma di installazione del driver.  
  
 *Zdroje dat* sono i database o i file aperti da un driver e sono identificati da un nome di origine dati (DSN). Utilizzare Amministrazione origine dati ODBC per aggiungere, configurare ed eliminare origini dati dal sistema. Nella tabella seguente sono descritti i tipi di origini dati che possono essere utilizzate.  
  
|Origine dati|Descrizione|  
|-----------------|-----------------|  
|Utente|I DSN utente sono locali rispetto a un computer e possono essere usati solo dall'utente corrente. Vengono registrati nel sottoalbero del Registro di sistema HKEY_CURRENT_USER.|  
|Sistema|DSN di sistema sono locali rispetto a un computer anziché dedicato a un utente. Il sistema o qualsiasi utente con privilegi possa utilizzare un'origine dati impostato con un DSN di sistema. DSN di sistema vengono registrati nel sottoalbero HKEY_LOCAL_MACHINE del Registro di sistema.|  
|File|DSN file sono origini basate su file che possono essere condivisi tra tutti gli utenti che hanno gli stessi driver installati, quindi hanno accesso al database. Queste origini dati non devono essere dedicate a un utente né essere in un computer locale. Nomi delle origini dati di file non vengono identificate dalle voci del Registro di sistema dedicata; al contrario, vengono identificati da un nome di file con estensione. DSN.|  
  
 Origini dati utente e di sistema sono noti collettivamente come *machine* origini dei dati perché sono locali in un computer.  
  
 Ognuna di queste origini di dati include una scheda nella **Amministrazione origine dati ODBC** nella finestra di dialogo. Per altre informazioni sulle origini dati, vedere [Origini dati](../../odbc/reference/data-sources.md).
