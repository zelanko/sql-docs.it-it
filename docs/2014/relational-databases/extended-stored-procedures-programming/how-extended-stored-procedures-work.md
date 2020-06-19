---
title: Funzionamento delle stored procedure estese | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 75082fed6b70c214b4f55b85034ffa371824d24f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027134"
---
# <a name="how-extended-stored-procedures-work"></a>Funzionamento delle stored procedure estese
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 Il funzionamento di una stored procedure estesa è il seguente:  
  
1.  Quando un client esegue una stored procedure estesa, la richiesta viene trasmessa nel formato TDS (Tabular Data Stream) o Simple Object Access Protocol (SOAP) dall'applicazione client a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue la ricerca della DLL associata alla stored procedure estesa e, se non è già caricata, la carica.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chiama la stored procedure estesa richiesta (implementata come funzione all'interno della DLL).  
  
4.  La stored procedure estesa passa set di risultati e restituisce parametri al server mediante l'API Stored procedure estesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione di stored procedure estese del Motore di database](../database-engine-extended-stored-procedure-programming.md)  
  
  
