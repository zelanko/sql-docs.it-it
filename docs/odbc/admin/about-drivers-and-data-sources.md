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
ms.openlocfilehash: 4e9b7229882b3b7f94e6b059e04c6496bde09641
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938047"
---
# <a name="about-drivers-and-data-sources"></a>Informazioni su driver e origini dati
I *driver* sono i componenti che elaborano le richieste ODBC e restituiscono i dati all'applicazione. Se necessario, i driver modificano la richiesta di un'applicazione in un modulo riconosciuto dall'origine dati. Per aggiungere o eliminare un driver dal computer, è necessario utilizzare il programma di installazione del driver.  
  
 Le *origini dati* sono i database o i file a cui accede un driver e sono identificati da un nome dell'origine dati (DSN). Utilizzare Amministrazione origine dati ODBC per aggiungere, configurare ed eliminare origini dati dal sistema. I tipi di origini dati che è possibile utilizzare sono descritti nella tabella seguente.  
  
|Origine dati|Descrizione|  
|-----------------|-----------------|  
|Utente|I DSN utente sono locali in un computer e possono essere usati solo dall'utente corrente. Sono registrati nel sottoalbero del registro di sistema HKEY_CURRENT_USER.|  
|Sistema|I DSN di sistema sono locali rispetto a un computer anziché dedicati a un utente. Il sistema o qualsiasi utente con privilegi può utilizzare un'origine dati configurata con un DSN di sistema. I DSN di sistema vengono registrati nel sottoalbero del registro di sistema HKEY_LOCAL_MACHINE.|  
|File|I DSN di file sono origini basate su file che possono essere condivise tra tutti gli utenti con gli stessi driver installati e pertanto avere accesso al database. Queste origini dati non devono essere dedicate a un utente né essere locali in un computer. I nomi delle origini dati del file non sono identificati da voci del registro di sistema sono invece identificati da un nome file con estensione DSN.|  
  
 Le origini dati utente e di sistema sono note collettivamente *come origini dati del computer perché* sono locali in un computer.  
  
 Ognuna di queste origini dati dispone di una scheda nella finestra di dialogo **Amministrazione origine dati ODBC** . Per altre informazioni sulle origini dati, vedere [Origini dati](../../odbc/reference/data-sources.md).
