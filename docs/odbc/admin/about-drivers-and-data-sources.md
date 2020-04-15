---
title: Informazioni sui driver e sulle origini dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dffeea3bea7e3fbfa66e534ecaa758fbc2064d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307222"
---
# <a name="about-drivers-and-data-sources"></a>Informazioni su driver e origini dati
*I driver* sono i componenti che elaborano le richieste ODBC e restituiscono dati all'applicazione. Se necessario, i driver modificano la richiesta di un'applicazione in un modulo riconosciuto dall'origine dati. È necessario utilizzare il programma di installazione del driver per aggiungere o eliminare un driver dal computer.  
  
 *Le origini dati* sono i database o i file a cui accede un driver e sono identificati da un nome di origine dati (DSN). Utilizzare Amministrazione origine dati ODBC per aggiungere, configurare ed eliminare origini dati dal sistema. I tipi di origini dati che è possibile utilizzare sono descritti nella tabella seguente.  
  
|Origine dati|Descrizione|  
|-----------------|-----------------|  
|Utente|I DSN utente sono locali a un computer e possono essere utilizzati solo dall'utente corrente. Sono registrati nella sottostruttura del Registro di sistema HKEY_CURRENT_USER.|  
|Sistema|I DSN di sistema sono locali rispetto a un computer anziché dedicati a un utente. Il sistema o qualsiasi utente con privilegi può utilizzare un'origine dati configurata con un DSN di sistema. I DSN di sistema vengono registrati nella sottostruttura del Registro di sistema HKEY_LOCAL_MACHINE.|  
|File|DSN su file sono origini basate su file che possono essere condivise tra tutti gli utenti che hanno installato gli stessi driver e pertanto hanno accesso al database. Queste origini dati non devono essere dedicate a un utente né essere locali a un computer. I nomi delle origini dati dei file non sono identificati da voci del Registro di sistema dedicate; al contrario, sono identificati da un nome di file con estensione dsn.|  
  
 Le origini dati utente e di sistema sono note collettivamente come origini dati *macchina* perché sono locali in un computer.  
  
 Ognuna di queste origini dati dispone di una scheda nella finestra di dialogo **Amministratore origine dati ODBC.** Per altre informazioni sulle origini dati, vedere [Origini dati](../../odbc/reference/data-sources.md).
