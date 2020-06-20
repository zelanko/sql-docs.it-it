---
title: Il motore di ricerca full-text Microsoft per SQL Server non caricherà i componenti di terze parti non firmati per impostazione predefinita | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 12ff188fb6aa6ac286817a7cc1c3ad726483c886
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012480"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>Per impostazione predefinita, il motore di ricerca full-text Microsoft per SQL Server non carica componenti di terze parti non firmato
  Per impostazione predefinita, il motore di ricerca full-text [!INCLUDE[msCoName](../../includes/msconame-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non carica componenti non firmati da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="component"></a>Componente  
 Ricerca full-text  
  
## <a name="description"></a>Descrizione  
 Per impostazione predefinita, dopo l'aggiornamento, un filtro di terze parti, ad esempio un filtro PDF, attualmente installato nel server non viene caricato nel motore di ricerca full-text [!INCLUDE[msCoName](../../includes/msconame-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per caricare un filtro di terze parti, è necessario impostare *load_os_resource* e disattivare *verify_signature* su tale istanza.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
