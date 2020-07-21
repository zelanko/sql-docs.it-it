---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cc0a085886dbec7eb8e5656bd7f84b9a066a3e4f
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552169"
---
# <a name="mssqlserver_21862"></a>MSSQLSERVER_21862
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
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
  
  
