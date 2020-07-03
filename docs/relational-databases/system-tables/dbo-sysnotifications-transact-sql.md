---
title: Notifiche dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b6ac4c1c037c186e1fe6fc20ad1b3ef0cfba976
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890427"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni notifica.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|ID dell'avviso.|  
|**operator_id**|**int**|ID dell'operatore a cui deve essere inviata la notifica.|  
|**notification_method**|**tinyint**|Metodo di notifica:<br /><br /> **1** = posta elettronica<br /><br /> **2** = cercapersone<br /><br /> **4**  =  **NetSend**<br /><br /> **7** = tutto|  
  
  
