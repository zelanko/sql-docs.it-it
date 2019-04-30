---
title: Comando TABLE DROP | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0865502928e98329764ae6085ab2b67aa26f0517
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128020"
---
# <a name="drop-table-command"></a>DROP TABLE (comando)
Rimuove una tabella dal database indicato con l'origine dati e lo elimina dal disco.  
  
 Il Driver ODBC Visual FoxPro supporta la sintassi del linguaggio Visual FoxPro nativa per questo comando. Per informazioni specifiche del driver, vedere la sezione Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Impostazioni  
 *TableName*  
 Specifica la tabella da rimuovere dal database indicato con l'origine dati ed eliminare dal disco.  
  
 *FileName*  
 Specifica una tabella gratuita per eliminare dal disco.  
  
 ?  
 Consente di visualizzare la finestra di dialogo di rimozione dalla quale è possibile scegliere una tabella da rimuovere dal database indicato con l'origine dati ed eliminare dal disco.  
  
## <a name="remarks"></a>Note  
 Quando viene eseguita l'istruzione DROP TABLE, vengono rimossi anche tutti i indici primari, i valori predefiniti e regole di convalida associate alla tabella. DROP TABLE influisce anche su altre tabelle nel database specificato con l'origine dati, se tali tabelle includono le regole o le relazioni associate alla tabella da rimuovere. Le regole e relazioni non sono più valide quando la tabella verrà rimossa dal database.  
  
## <a name="driver-remarks"></a>Sezione Osservazioni di driver  
 Quando l'applicazione invia l'istruzione ODBC SQL DROP TABLE per l'origine dati, il Driver ODBC Visual FoxPro converte il comando al comando Visual FoxProDROP tabella utilizzando la sintassi illustrata nella tabella seguente.  
  
|Sintassi ODBC|Origine dati|Sintassi di Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *nome-tabella di base*|Database (file DBC)|Per rimuovere una tabella *TableName* DELETE|  
||Directory delle tabelle gratuite (file con estensione dbf)|ERASE *dbfName*<br /><br /> ERASE *cdxName*<br /><br /> ERASE *fptName*|
