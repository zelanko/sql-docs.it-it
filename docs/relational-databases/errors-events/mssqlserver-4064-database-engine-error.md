---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 81537ea994fa22ee9cafb2ba031677a1d5544dcd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123370"
---
# <a name="mssqlserver_4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|4064|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DB_UFAIL_FATAL|  
|Testo del messaggio|Impossibile aprire il database utente predefinito. Accesso non riuscito.|  
  
## <a name="explanation"></a>Spiegazione  
L'account di accesso di SQL Server non è in grado di connettersi a causa di un problema con il relativo database predefinito. Il database non è valido oppure l'account di accesso non dispone dell'autorizzazione CONNECT per il database.  
  
## <a name="user-action"></a>Azione dell'utente  
Utilizzare ALTER LOGIN per modificare il database predefinito dell'account di accesso. Concedere l'autorizzazione CONNECT all'account di accesso.  
  
