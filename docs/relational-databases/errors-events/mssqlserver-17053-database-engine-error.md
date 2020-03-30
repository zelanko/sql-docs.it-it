---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d078557186af534f1f489e8fee2e0f803c548f58
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68100435"
---
# <a name="mssqlserver_17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17053|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|OS_ERROR|  
|Testo del messaggio|%ls: è stato rilevato l'errore del sistema operativo %ls.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un errore del sistema operativo generico.  Lo stato risultante non è chiaro.  
  
## <a name="user-action"></a>Azione dell'utente  
In genere questo errore si verifica con altri errori e deve essere utilizzato per consentire di diagnosticare gli errori specifici. Alcuni esempi potrebbero essere costituiti da letture o scritture in file di dati o di log non eseguite in modo corretto, da operazioni di lettura o scrittura nel Registro di sistema o da altri errori relativi all'API Win32 non previsti.  
  
