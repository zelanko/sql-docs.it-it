---
title: Altre annotazioni (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 668e26430e97a1e7d34e0e420966b975874224c0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750033"
---
# <a name="other-annotations-sqlxml-40"></a>Altre annotazioni (SQLXML 4.0)
  Oltre alle annotazioni descritte negli argomenti precedenti di questa sezione, il caricamento bulk XML interpreta queste altre annotazioni, come segue:  
  
 `sql:id-prefix`  
 Se lo schema specifica i prefissi dei dati XML, il caricamento bulk XML rimuove i prefissi prima di inviare i dati a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:use-cdata`  
 Il caricamento bulk XML legge il testo archiviato nelle sezioni CDATA e lo invia a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:url-encode`  
 Il caricamento bulk XML non supporta questa annotazione. Non è possibile ad esempio specificare un URL nei dati XML di input e prevedere che il caricamento bulk XML legga i dati da tale posizione per archiviarli nel database.  
  
 `sql:is-mapping-schema`  
 Il caricamento bulk XML non supporta questa annotazione né supporta `sql:id`.  
  
> [!NOTE]  
>  Il caricamento bulk XML non supporta schemi di mapping inline.  
  
 `sql:key-fields`  
 Il caricamento bulk XML ignora sempre questa annotazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Interpretazione di annotazione &#40;SQLXML 4.0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
