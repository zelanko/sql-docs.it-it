---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 03c0ffb40a5472de7d2fea1730eebe192430406f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056724"
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|MSSQLSERVER|  
|ID evento|21862|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21862|  
|Testo del messaggio|Impossibile pubblicare le colonne FILESTREAM in una pubblicazione con metodo di sincronizzazione 'database snapshot' o 'database snapshot character'.|  
  
## <a name="explanation"></a>Spiegazione  
Poiché non è possibile accedere ai dati FILESTREAM tramite uno snapshot del database, l'agente snapshot non sarà in grado di leggere dati FILESTREAM se viene specificato il parametro *database snapshot* o *database_snapshot_character* per il metodo di sincronizzazione della pubblicazione.  
  
## <a name="user-action"></a>Azione dell'utente  
Impostare il metodo di sincronizzazione di pubblicazione su un valore diverso da *database snapshot* o *database_snapshot_character* oppure escludere la colonna FILESTREAM dalla pubblicazione.  
  
